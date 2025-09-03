---
{"dg-publish":true,"permalink":"/projects/game of life/game of life with logic gates/"}
---

#projects/game_of_life 
as the title said it: we are going to play the game of life in logic gate simulator
# the start
this idea came to me with a video of building working memory in logic gate sim.
what i thought to do in the start was building a full mini pc and code it to run the game of life. and it is still the plan but we scale it down a bit
## step one assert dominant on the logic gate system
for this we going to learn how to code memory for 3 thing.
- long memory for the holding of the cells of the game
- short for doing the calculations
- long for having the procedure
after this we going to have mini CPU to run calculations in the most basic form
plus minus and then more complicated once like multiply and deviations.
## the rules of game of life
https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life
1. Any live cell with fewer than two live neighbours dies, as if by underpopulation.
2. Any live cell with two or three live neighbours lives on to the next generation.
3. Any live cell with more than three live neighbours dies, as if by overpopulation.
4. Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.
this is pretty much it
simple yet amazing
## procedure
this is the most difficult part in the project. how can we right code that fit our architect. lets start by setting the stage.
### set the stage
this stage loop the cpu procedure to wait to human instruction. those being: decide if cell is populated (1) or not (0).
after the human press button to start the sim. the app move to the next stage. 
### sim
it goes by every cell check it neighbors. 
remember the long time storage. ye this one it old data of cell and if it a live or not. then check by pointers to see what is going next to it.
then return value to be updated.
# known problems
## software
lets start by saying, yes i know its heavy and i mean **really heavy** compare to what to software does in the day by day, so obviously I'm going to get hate from the software and also my pc.

but that not the only issue with software; right now the known problem, or at list just for me is: single bus kinda not working. 
what to do? for start we could change the memory build to fit this issue 
*see pic before and new*

# there is a second solution
yes there is... kinda. we could code this entire thing in logic gate. the same why coding screen to work with numbers
see 7 segment screen configure

one way which im might work with.
every single pixel is input and out put.
one clock trigger, the cell being checked by simple input of: 1 middle cell and 8 surrounding pixels. it do some logic gate shit which is optimized with [Karna maps](https://en.wikipedia.org/wiki/Karnaugh_map) and output `1` or `0` to fill the middle pixel. rents and repeat.
**pros**: easy, only one chip needed to be design.
**cons**: I'm sure there going to be a lot of problem because you check all cells in one clock trigger, and that pretty much it.
I'm not going to use it and leave it as lust resource.
# lets begin 
for starters before even jumping in full head I'm still going to need to clear a lot of unknown subject. like how to create mini CPU.
the CPU pretty much going to get code and process it and give result. but because we work with only one goal in mind, that it "game of life" there is no need to build the entire infostructure.
[[game of life.canvas|game of life]]
![game of life.webp](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/game%20of%20life.webp)
this is the basic form of the... lets call it device.
**start** - is the input to start the action
**initiator** - can write into *screen memory* 1 or 0. then refresh screen to show the game before starting the sim. then when user ready, press continue send 1 to clock. making the sim start running in loop.
**screen memory** - hold memory of the game
**CPU** - i might combine it with instruction. but is job is run on each cell and check the surrounding of the cell with the [[#the rules of game of life|game of life instructions]]
**printer** - make sure to print the screen each time.

# 8 bit decoder to 3X4bit 
8 bit or more known 1 byte. have 0-255 or -128 to 127 or 256 values, depend where you start the count. to be translated to decimals to be display we first turn the number in 8 bit to 3 numbers with 4 for each digit.
to do it we need to understand, 0-9 digit presented by 4 bit but also 10-15 which mean 6 result which have no use for us and can make thing harder.
to fix it we take each one of them (10-15) and translate them to the equivalent in 0-9 with addition of 6:
$10+6 = 0$
...
$15+6= 5$
after researching it a little bit i could find the solution is double dabble logic gate.
which mean to add 3... and not 6... wait a second. ill read it come right back.
## double dabble
ok so im done reading and made full double dabble chip with 8bit entry and 3X4bit out put.
if you want to see the math behind the chip: 
```
0000 0000 0000   11110011   Initialization
0000 0000 0001   11100110   Shift
0000 0000 0011   11001100   Shift
0000 0000 0111   10011000   Shift
0000 0000 1010   10011000   Add 3 to ONES, since it was 7
0000 0001 0101   00110000   Shift
0000 0001 1000   00110000   Add 3 to ONES, since it was 5
0000 0011 0000   01100000   Shift
0000 0110 0000   11000000   Shift
0000 1001 0000   11000000   Add 3 to TENS, since it was 6
0001 0010 0001   10000000   Shift
0010 0100 0011   00000000   Shift
   2    4    3
       BCD
```
https://en.wikipedia.org/wiki/Double_dabble
where the dabble chip: ![dabble chip +3 with gates.webp|526](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/dabble%20chip%20+3%20with%20gates.webp)
*ye i know i can optimize it. but it took me way to much tries so NO!*
this one just add 3 if its over 5 (see excel double dabble)
then orginzie them in this pattern:![double dabble chip build.webp](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/double%20dabble%20chip%20build.webp)
and boom!!! side quest which took TOO much time.
![double dabble look with 3 7 seg dis.webp](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/double%20dabble%20look%20with%203%207%20seg%20dis.webp)
you can see it work like charm. *this is the not final form*
![sim dis slow my laptop.webp](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/sim%20dis%20slow%20my%20laptop.webp)
we can all ready see my laptop crumbling just under the load of this small demonstration.
# CPU
do you know [scott's CPU](https://sim4edu.com/sims/26/Scott-8-bit-computer) its the most basic CPU you can build out of logic gate, the CPU can run all basic functions, and can be coded with assembly and compile to binary.
the CPU run in 8 clock loop: one function (read, process and store) in 8 clock run
math time: if the sim run in 80 loops in sec that 10 function per sec.
but because we all ready tanking our sim to 89 i expect it to slow up to 1 function per sec
LAME
if i run it on my big (gamer) pc maybe i can squeeze more then 1 per sec.
just so you understand, just one pixel check take up to 9 functions, just for the check.
for start we going to make our version of CPU
reasons:
- i want to learn- not copy
- we might find a way to ease the sim load using build in chips (they are more optimize and not running fully on logic gate made of NAND)
you need to remember all gate, all chips in this sim are made of NAND 
so something simple as the Double Dabble from before using 100's if not 1000's of NAND running all on the sim and getting visual printed.
its a plus to have visual sim but its also the minus when you want to go big.
# oriented circuit
the oriented circuit run clock with fazes for each "line of code"
[[projects/game of life/create faze list for the cpu\|create faze list for the cpu]]
# clean mod
if "sim" is not running and the cpu run on "prep" mod then you can switch on switch for "clean".
in "clean" mod the chip run on each memory in the screen memory and change them all to 0. so the user would have clean screen for the next simulation.
[[clean mod.canvas|clean mod]]
# prep mod
in the prep mod user run each user input. 
move memory cell (screen cell) left, right, up, down.
and decide if it light up (1) or not (0).
[[prep mod.canvas|prep mod]]
# next step
we going to start with prep mod.
the chip is not clock related making it easy
input:
5 buttons
out put:
memory bus
asign base
## inputs
1. left
2. right
3. up
4. down
5. asign
## output
1. 8 bit bus for memory
2. 1 bit bus for the data of the memory
