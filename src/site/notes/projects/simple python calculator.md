---
{"dg-publish":true,"permalink":"/projects/simple python calculator/"}
---

# lets begin
I started with tkinter from python
see [tutorial](https://www.pythontutorial.net/tkinter)
moved to setting the grid
only what is in square is what im making
![image.png|343x418](/img/user/image.png)
# griding
se we need grid of:
columns: 4
rows: 5
end up with this
![image-1.png|300x339](/img/user/image-1.png)
# code
## sharpen the UI
```python title:"platform check"
# platform
if platform.system() == "Windows":
    try:
        from ctypes import windll

        windll.shcore.SetProcessDpiAwareness(1)
    except Exception:
        pass
```
this ensure that if the OS is windows then the system will run 
`SetProcessDpiAwareness` to sharpen the UI.
[![resolution test](https://private-user-images.githubusercontent.com/45383191/309088909-3600983c-4754-448f-aa80-cea456b040c6.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTUyMDU2NTAsIm5iZiI6MTc1NTIwNTM1MCwicGF0aCI6Ii80NTM4MzE5MS8zMDkwODg5MDktMzYwMDk4M2MtNDc1NC00NDhmLWFhODAtY2VhNDU2YjA0MGM2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA4MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwODE0VDIxMDIzMFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTE3YjQyNzBmYTkzNmQ3OTM1MjU5ZWEwMDQ2YzgxNzA4MjdkYjAzYjEzZGZiYWEyNjFhNjlmOWYyN2FmYTQxMzEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.muzzt0XPsMkBmUwN8lbZyjPkjc8tEYUjfb5a5L0N_WA)](https://private-user-images.githubusercontent.com/45383191/309088909-3600983c-4754-448f-aa80-cea456b040c6.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTUyMDU2NTAsIm5iZiI6MTc1NTIwNTM1MCwicGF0aCI6Ii80NTM4MzE5MS8zMDkwODg5MDktMzYwMDk4M2MtNDc1NC00NDhmLWFhODAtY2VhNDU2YjA0MGM2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA4MTQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwODE0VDIxMDIzMFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTE3YjQyNzBmYTkzNmQ3OTM1MjU5ZWEwMDQ2YzgxNzA4MjdkYjAzYjEzZGZiYWEyNjFhNjlmOWYyN2FmYTQxMzEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.muzzt0XPsMkBmUwN8lbZyjPkjc8tEYUjfb5a5L0N_WA)
left: without resolution setting  
right: set system resolution
[SetProcessDpiAwareness](https://www.reddit.com/r/Tkinter/comments/pp1n6o/font_blur_in_the_gui)
## lay the grid
```python
# set the grid and make it flex
def set_cal_grid(root):
    root.rowconfigure(0, weight=2)
    root.rowconfigure(1, weight=1)
    root.rowconfigure(2, weight=1)
    root.rowconfigure(3, weight=1)
    root.rowconfigure(4, weight=2)
    root.columnconfigure(4)
    for i in range(5):
        root.grid_rowconfigure(i, weight=1)
        pass
    for i in range(4):
        root.grid_columnconfigure(i, weight=1)
        pass
```
this lay the grid but also config it to be flexible with all the buttons changing sizes to fit.
## get number
```python
def press(value):
    global reg_1
    reg_1 += str(value)
    entry.config(text=reg_1)
```
when a button of 0-9 press this add it to the the str of numbers
## get action
```python
def act(action):
    global reg_1,reg_tmp,a
    reg_tmp = reg_1
    a = action
    reg_1 = ""
```
get the  user action from button and update `a`. clear the reg_1 for new input.
## get result
```python
def result():
    global reg_1,reg_tmp,a,res
    #print(f"reg_temp before:{reg_tmp}")#debug
    if reg_tmp =="":
        reg_tmp = res
    if a == '+':
        res = int(reg_tmp)+int(reg_1)
        entry.config(text=str(res))
        reg_tmp = ""
    elif a == '-':
        res = int(reg_tmp)-int(reg_1)
        entry.config(text=str(res))
        reg_tmp = ""
    elif a == '/':
        if reg_1 != 0:
            res = int(reg_tmp)/int(reg_1)
            entry.config(text=str(res))
            reg_tmp = ""
        else:
            res = 0
            entry.config(text=str(res))
            reg_tmp = ""
    elif a == '*':
        res = int(reg_tmp)*int(reg_1)
        entry.config(text=str(res))
        reg_tmp = ""
    #print(f"reg_1:{reg_1},reg_temp:{reg_tmp},res:{res},action:{a}")#debug
```
the code take the global variables and combine them based on the `a` of action
## main
```python
if __name__ == "__main__":
    root = tk.Tk()  # create window
    screensize_width = root.winfo_screenwidth()  # get screen size
    screensize_height = root.winfo_screenheight()  # get screen size
  

    center_x = int(screensize_width / 2 - win_width / 2)  # find center with window size
    center_y = int(screensize_height / 2 - win_height / 2)
    set_cal_grid(root)  # create grid


    
    entry = ttk.Label(text=reg_1)  # create an display
    entry.grid(column=0,row=0,columnspan=4)
    reg_1 = ""
    reg_tmp = ""
    res = ""
    a = ''
    # the 2 numbers for the calculator
  
    # start button
    button_1 = ttk.Button(text="1",command=lambda: press(1))
    button_2 = ttk.Button(text="2",command=lambda: press(2))
    button_3 = ttk.Button(text="3",command=lambda: press(3))
    button_4 = ttk.Button(text="4",command=lambda: press(4))
    button_5 = ttk.Button(text="5",command=lambda: press(5))
    button_6 = ttk.Button(text="6",command=lambda: press(6))
    button_7 = ttk.Button(text="7",command=lambda: press(7))
    button_8 = ttk.Button(text="8",command=lambda: press(8))
    button_9 = ttk.Button(text="9",command=lambda: press(9))
    button_0 = ttk.Button(text="0",command=lambda: press(0))
    button_res = ttk.Button(text="=",command=result)
    button_add = ttk.Button(text="+",command=lambda: act('+'))
    button_minus = ttk.Button(text="-",command=lambda: act('-'))
    button_devide = ttk.Button(text="/",command=lambda: act('/'))
    button_multi = ttk.Button(text="*",command=lambda: act('*'))

    # place button
    button_1.grid(column=0, row=1, sticky="nsew")
    button_2.grid(column=1, row=1, sticky="nsew")
    button_3.grid(column=2, row=1, sticky="nsew")
    button_4.grid(column=0, row=2, sticky="nsew")
    button_5.grid(column=1, row=2, sticky="nsew")
    button_6.grid(column=2, row=2, sticky="nsew")
    button_7.grid(column=0, row=3, sticky="nsew")
    button_8.grid(column=1, row=3, sticky="nsew")
    button_9.grid(column=2, row=3, sticky="nsew")
    button_0.grid(column=0, row=4, sticky="nsew")
    button_add.grid(column=3, row=1, sticky="nsew")
    button_minus.grid(column=3, row=2, sticky="nsew")
    button_devide.grid(column=3, row=3, sticky="nsew")
    button_multi.grid(column=3, row=4, sticky="nsew")
    button_res.grid(column=1, row=4, sticky="nsew", columnspan=2)
  

    # title this shit
    root.title("calculator")
    root.iconbitmap("Calculator_30001.ico")
    # display window on screen
    root.geometry(f"{win_width}x{win_height}+{center_x}+{center_y}")
    # lets roll
    root.mainloop()
```
### lets break the main to parts
`if __name__ == "__main__":` means to run only when this code is the main. make it so other python programs cant run this code and only the `def` inside of it.
mostly to make it so the programs running python on VScode doesn't clash into each other.
`root = tk.Tk()  # create window` create a window and call it `root`
```python
screensize_width = root.winfo_screenwidth()  # get screen size
screensize_height = root.winfo_screenheight()  # get screen size
```
get the user screen resolution (so i can place it the middle of the screen)

```python
center_x = int(screensize_width / 2 - win_width / 2)  # find center with window size
center_y = int(screensize_height / 2 - win_height / 2)
```
this part find the edge of the root window  from the center
![image-4.png|340x404](/img/user/image-4.png)
where (1_red) is the center
`set_cal_grid(root)  # create grid` create a grid in the window `root`
```python
entry = ttk.Label(text=reg_1)  # create an display
entry.grid(column=0,row=0,columnspan=4)
```
create a `Label` of `ttk` to display the numbers you type and the res
call it `entry` then display it in the grid and let it spread all the top row
`columnspan` tell the obj (ttk) how many grid cells he can take. in this example it take 4 which is all the columns in the grid we created


```python
reg_1 = ""
reg_tmp = ""
res = ""
a = ''
```
create all the variables/ holders. `reg_1` is the one you type to. `reg_temp` is the one hold `reg_1` while you get the second number and wait for the result.
`res` hold the result, useful for doing more then one operation
`a` hold the action

```python
# start button
    button_1 = ttk.Button(text="1",command=lambda: press(1))
    button_2 = ttk.Button(text="2",command=lambda: press(2))
    button_3 = ttk.Button(text="3",command=lambda: press(3))
    button_4 = ttk.Button(text="4",command=lambda: press(4))
    button_5 = ttk.Button(text="5",command=lambda: press(5))
    button_6 = ttk.Button(text="6",command=lambda: press(6))
    button_7 = ttk.Button(text="7",command=lambda: press(7))
    button_8 = ttk.Button(text="8",command=lambda: press(8))
    button_9 = ttk.Button(text="9",command=lambda: press(9))
    button_0 = ttk.Button(text="0",command=lambda: press(0))
    button_res = ttk.Button(text="=",command=result)
    button_add = ttk.Button(text="+",command=lambda: act('+'))
    button_minus = ttk.Button(text="-",command=lambda: act('-'))
    button_devide = ttk.Button(text="/",command=lambda: act('/'))
    button_multi = ttk.Button(text="*",command=lambda: act('*'))
```
this code create the button and give them factuality
let break it down:
	`button_1 = ttk.Button`: create a `ttk` `button` and assign it a pointer for later use
	`text="1"`:display a text on the button (default format)
	`command=lambda: press(1)`: assign the button function using [lambda](https://www.w3schools.com/python/python_lambda.asp)

```python
# place button
    button_1.grid(column=0, row=1, sticky="nsew")
    button_2.grid(column=1, row=1, sticky="nsew")
    button_3.grid(column=2, row=1, sticky="nsew")
    button_4.grid(column=0, row=2, sticky="nsew")
    button_5.grid(column=1, row=2, sticky="nsew")
    button_6.grid(column=2, row=2, sticky="nsew")
    button_7.grid(column=0, row=3, sticky="nsew")
    button_8.grid(column=1, row=3, sticky="nsew")
    button_9.grid(column=2, row=3, sticky="nsew")
    button_0.grid(column=0, row=4, sticky="nsew")
    button_add.grid(column=3, row=1, sticky="nsew")
    button_minus.grid(column=3, row=2, sticky="nsew")
    button_devide.grid(column=3, row=3, sticky="nsew")
    button_multi.grid(column=3, row=4, sticky="nsew")
    button_res.grid(column=1, row=4, sticky="nsew", columnspan=2)
```
for each button i created i assign cell in grid and also config it
lets break it down:
	`button_1.grid`:on this button config grid
	`column=0, row=1,`:which cell
	`sticky="nsew"`:fill the entire cell. [you can make it stick and fill only one side or just the bottom or top](https://www.pythontutorial.net/tkinter/tkinter-grid/#sticky)

```python
# title this shit
root.title("calculator")
```
give the window we created a title. the title will be display on the top bar of the window.
`root.iconbitmap("Calculator_30001.ico")` give the window an icon
![image-5.png](/img/user/image-5.png)
```python
# display window on screen
root.geometry(f"{win_width}x{win_height}+{center_x}+{center_y}")
```
finally we display the window with the calculation we made to spawn it in the middle of the screen.

```python
#lets roll
root.mainloop()
```
and let not forget to loop it 
if we not going to do it the window will be created and then close as soon as opened.

# cancelation
is tkinter good.
i mean it is fine. but it take time to get used to.
and holy shit do i hate global variables (only use them when coding in arduino)
i really need to find a better way to make it.
some things feel smooth to create in python
and other things... FUCK ME
so if ill take something from here is: if you want to create a small UI then its perfect especially if your vibe. is win xp settings.
i do see my self making more stuff with it.
but i need to figure a better way to run functions with it which doesn't include global. 

[[tkinter base for the calculator.canvas|tkinter base for the calculator]]
![tkinter base for the calculator.png](/img/user/tkinter%20base%20for%20the%20calculator.png)
[icons](https://icon-icons.com)
