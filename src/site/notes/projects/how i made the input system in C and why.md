---
{"dg-publish":true,"permalink":"/projects/how i made the input system in C and why/"}
---

#cabinet/blog #study/coding/C 
in this part we are going to dive only into one part of my code, see what good what bad and most of all why
we are going to examine the system to details and seeing where i could improve and how
we are also going to talk about a very important idea, microservice-like function and API
# let begin
```c title:get_user_action
char* get_user_action()
{
    char buffer[255] = {'\0'};
    fgets(buffer,255,stdin);
    char action[128] = {'\0'};
    char abuse[128] = {'\0'};
    char pointer[128] = {'\0'};
    short i = 0;
    
    while (buffer[i] != '\0')
    {
        buffer[i] = tolower(buffer[i]);
        i++;
    }
    if (!strcmp(buffer, "help\n")) { print_help(); return NULL; }
    sscanf(buffer,"%s %s %[^\n]",&action,&abuse,&pointer);
    char action_c = get_action(action);
    if(action_c == '`'){error_no_action();}
    if(abuse[0]=='\0')
    {
        error_no_abuse(action_c);
        return NULL;
    }
    char abuse_c = get_abuse(abuse);
    char sys_a[3] = {'\0'};
    sys_a[0] = action_c;
    sys_a[1] = abuse_c;
    char* final;
    char* new_pointer;
    if(pointer[0] == '\0')
    {
        new_pointer = get_pointer(action_c,abuse_c);
    }else
    {
        new_pointer = malloc(sizeof(char)*(strlen(pointer)+1));
        strcpy(new_pointer, pointer);
    }
    final = malloc(sizeof(char) * (strlen(sys_a) + strlen(new_pointer) + 1));
    i = 0;
    while (final[i] != '\0')
    {
        final[i] = '\0';

    }
    strcat(final, sys_a);
    strcat(final, new_pointer);
    free(new_pointer);
    return final;
}
```
its all begin with this terrifying function but worry ill explain each part
first with initiate all the parameter and holder
```c title:init
	char buffer[255] = {'\0'}; //for user input
    fgets(buffer,255,stdin); //get user input
    char action[128] = {'\0'}; //for the action
    char abuse[128] = {'\0'}; //for the abuse(file or folder)
    char pointer[128] = {'\0'}; //pointer (str) to (file or folder)
    short i = 0; //counter for a few parts
```
after we initiate the holders and buffer and also get user string with `fget`
we lower the entire input to lowercase
so the function will not be case sensitive
>[!note]
>i could have made it so only the action and abuse will be non case sensitive

```c title:to_lower
while (buffer[i] != '\0')
{
    buffer[i] = tolower(buffer[i]);
    i++;
}
```
i used `tolower` from `ctype.h` but i could have just ASCII hacked my way to lower casing
then i simply checked on the buffer (user input) to see if the user asked for `help`. if so print the help function 
```c title:help_fuction
void print_help()
{
    printf("action abuse pointer\naction:\n");
    printf("    create file: -c / create \n");
    printf("    delete file: -d / delete \n");
    printf("    open file: -o / -> / open \n");
    printf("abuse:\n");
    printf("    file: f / file \n");
    printf("    folder: a / folder \n");
    printf("pointer: str or int\n");
}
```
{ #2b5cfe}


after this, split the buffer to 3 parts: ` {str} {str} {rest of characters}`.
`    sscanf(buffer,"%s %s %[^\n]",&action,&abuse,&pointer);` 
first string is: action
second string: abuse
rest of char str: pointer
>[!info]
>the `%s` from scanf scan until space. which is diffrent then what you expect.
>if you want to take few strings you could `%[^\n]` which mean take all char until you see `\n`

after this we get the action which could be in couple of form (see [[#^2b5cfe|help]]) and return one `char` .
over all very confusing. so you shouldn't try dig too deep. 
in short the function search for either a `-` and then `char` or an exact match of string.
```c title:"get action"
char get_action(char *action)
{
    if(action[0] == '-')
    {
        switch (action[1])
        {
        case 'c': //create
            return 'c';
            break;
        case 'd': //delete
            return 'd';
            break;
        case 'o': //open
            return 'o';
            break;
        case '>': //open
            return 'o';
            break;
        default:
            return '`';
            break;
        }
    }else if (action[0] == '/')
    {
        if (action[1] == '/')
        {
            return '|'; //back to C:
        }
        else
        {
            return '/'; //back one folder
        }
    }else
    {
        if (!strcmp(action,"create"))
        {
            return 'c';
        }else if (!strcmp(action,"delete"))
        {
            return 'd';
        }else if (!strcmp(action,"open"))
        {
            return 'o';
        }else if (!strcmp(action,"sys"))
        {
            return '*'; //system
        }else{return '`';}
        
    }
}
```
if by any chance non match was found, the function return `'` which tell the software to print error `error_no_action`
it just print that you didn't enter action or entered it poorly 
next check to see if the user only entered one word
if so `error_no_abuse` is printed
next we do the same for the abuse
`get_abuse(abuse)` return on `char` corospond to either a file `f` or folder `a` [arcive]
```c title:sys_a
char sys_a[3] = {'\0'}; 
sys_a[0] = action_c;
sys_a[1] = abuse_c;
```
we create mini string for short storage
```c title:"get new pointer or get the pointer from buffer"
char* final;
char* new_pointer;
if(pointer[0] == '\0')
{
    new_pointer = get_pointer(action_c,abuse_c);
}else
{
    new_pointer = malloc(sizeof(char)*(strlen(pointer)+1));
    strcpy(new_pointer, pointer);
}
final = malloc(sizeof(char) * (strlen(sys_a) + strlen(new_pointer) + 1));
```
holder for `final` and `char` array of the final action code
and `new pointer` if the user have a pointer then this is copyed to the `new_pointer`
otherwise the user get the chance to give the missing pointer.
we check to see if user entered pointer by checking the first letter in the pointer array we got from the buffer.
finally we get the size of the final `char` array for the action code
```c title:final
strcat(final, sys_a);
strcat(final, new_pointer);
free(new_pointer);
return final;
```
then copy and free and send to the return
# what i could have fixed
the code is very long. sould have cut the `sys_a` 
i forgot to take care of `sys` and create this abomination
```c title:"quick fix"
    if (action_c == '*') { char* s = malloc(2 * sizeof(char)); if (!s) { return NULL; }; s[0] = '*'; s[1] = '\0'; return s; }
```
which figure if action is `sys` which is `*` and return only this
there too many useless variables and pointer which given enough time and dedication i could have fixed.
[[input pipeline.canvas|input pipeline]]
![input pipeline.png](/img/user/projects/input%20pipeline.png)
# but why
ho i glad you asked.
the real reason for all of this is
# API and microservice-like function
they act as a black box, microservice-like function. you give it unfiltered but followed by roles, commends and they return the same. formatted date according to the rules.
this is [API](https://en.wikipedia.org/wiki/API)
Application Programming Interface
which is a given set of rules for people that want to use your app.
ill give a great example i like
you have a machine, this machine store cookies. you want to use this machine. but you don't want to know how it works, only that it works. because the inside of this machine is complicated and terrifying.
so the manufacture create a set of rules. 
if you want a cookie simply write: get {number of cookies} {the type of cookie}
for example: get 1 chocolate cookie
so the basic rules are: {action} {number} {type}
this why the user get easy to use controls while also giving him full control.
this tactic i also use for my code. this way, when i finish with a mini function-struct like, the one i showed you, i know this part of the program is done. and as long as i don't need to change to program and as long as i follow the rules i set. the function will work no problem.
this is the reason way preparing the layout and borders of the app before hand helps a lot and make sure rewriting entire functions, and wasting time, is out of the table.
this is also very important when working in a team, this way even if i don't know how my friend created his function i can still use it.
# conclusion
- this is a microservice-like function meant to take large types of format and compress it to small restrict format for later use. 
- the function could use some improvement.
- we talked about microservice-like function and API and why when building even function for your own program its sometime better to use the API building set of rules.

[[cabinet/welcome_to_my_garden\|back to the web hub]] 🏡