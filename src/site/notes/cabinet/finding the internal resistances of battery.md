---
{"dg-publish":true,"permalink":"/cabinet/finding the internal resistances of battery/"}
---

in electrical engineering there are somethings which everyone learn at some point
in those kind of post ill try to to teach you those things and also give you real life examples, experiments and over all extend on the basic.
# the basic of the formula
everyone know this formula 
$V = IR$ 
this is the basic for all of amper-linear-like applications. those are resistance at all their form. this formula is not meant for other types which are not linear, like LED and diode
what you probably not fully remember is the full formula
$V_{ab} = \varepsilon -Ir = IR$
where: 
$\varepsilon -Ir$ - is internal resistance
{ #6ef85d}

# what is internal resistance
nothing is like the math we learn, there are imperfection. the wires in the drawing are called ideal wire with no resistance and no lost, but real life is diffrent, every material have resistance, some more (isolators) so very little (conductors) and some in between.
even inside the battery the electrons are moving though material, this cause the lose of energy. you can actually feel it every time you charge or use the battery, the battery heat up, this is a lose of energy to internal resistance.
in drawing especially you'll see the internal resistance presented as {$r$} and will be right beside the battery or power supply and they will be presented with the symbol {$\varepsilon$}
ill explain letter how can you find each one.
![image.png|386x194](/img/user/image.png)
# efficient 
this mean how much energy is lost not doing the work intended.
this  presented by this equation:
$$\eta = \frac{P_{out}}{P_{in}} = \frac{I^2(R)}{I^2(R+r)}=1-\frac{(r)}{(R+r)}$$
where you can see that if {$r$} is very small the efficiency of the circuit is very good and if is high then the efficiency is very low and their for bad.
i promise ill make a post on the reason behind the high voltage on power line, this is just great place to sag way to it.
# we can find $\varepsilon$
this feel like cheating the first time i heard it but its pretty simple. you can pass the need to calculate the {$r$} to calculate the {$\varepsilon$} and the reason is because when you measure voltage you are not measuring the movement of electrons but measure the potential of them to move. you can imagine it like the a water pump building pressure but not moving the water. the water is not moving but you can still measure its potential to who strong it will move. $V$ is the pressure $I$ is the speed in which the water move and $R$ is the size of the pipe its moving through. this is analogy everyone is using to explain the ropes of electricity.
because you are measuring the potential of electrons actually their charge, you are skipping the $I$ , current, and their for skipping the resistance as well.
feel like cheating ha
![image-1.png|example show casing how to find EMF electromagnetic force which is the battery voltage inside|347x231](/img/user/image-1.png) 
# find the internal
now that we have the components {$\varepsilon$} and $R$ we can find organize the equation
1. $\varepsilon =Ir + IR$ 
2. $\varepsilon =I(r + R)$
3. $I=\frac{\varepsilon }{r+R}$
no we found the $I$
we need to measure while the circut is connected for the current to flow
and find the other side
4. $V_{ab} = \varepsilon -Ir$ 
5. $\varepsilon -V_{ab} =Ir$
6. $r=\frac{\varepsilon -V_{ab}}{I}$
and that it we found it
you can then do it couple of times with diffrent setups to eliminate the imperfections in the measuring equipment
# real example
i created a circuit using a battery i had from an other project.
i only changed th e resistance and tested the V of the battery 
![image-2.png|you can see where i tested the V of the battery|364x363](/img/user/image-2.png)
i chose to resistors for the circuit:
- $R_1$ = 470$\pm$ 5% {$\Omega$}
- $R_2$ = 220$\pm$ 5% {$\Omega$}
next i check the voltage for each resistor
- $V_1$ = 8.07$\pm$ 0.05 {V}
- $V_2$ = 8.01$\pm$ 0.05 {V}
next i calculated the current for each time using $I = \frac{V}{R}$
- $I_1$ = 0.017170 {A}
- $I_2$ = 0.036409 {A}
then check the error for it using 
$$\Delta I = \sqrt{\left (  \frac{dI}{dV}\right )^{2}(\Delta V)^{2}}+\sqrt{\left ( \frac{dI}{dR} \right )^2(\Delta R)^2}$$
{ #35c216}

- $\Delta I_1 = \pm 1.08209\times _{10}^{-4}$ 
- $\Delta I_2 = \pm 2.35547\times _{10}^{-4}$ 
now ill combine them together in the [[#^6ef85d|other side of the formula]] 
$V = \varepsilon  - Ir$ 
now we left with
$V_1-V_2 = - (I_1-I_2)r$
and we can get $r$
$r = 3.1186$
to calculate the error we do [[#^35c216|it]] again
because the current is very low then the error by the derivative is very high
we bypass it by using current which is higher by increasing the voltage (which i would not do for safety reason) or lower the resistance this can be done but because i don't want  to make all the circuit part all over again ill just continue.
we can say the $\Delta r$ is very little
now that we have the $\Delta r$ we can insert it to one equation and find $\varepsilon$ 
$\varepsilon = 8.1235$ {V} 
## the circuit is simulation
here is a simulation of the 2 circuits
![circuit 1 (470R).gif](/img/user/circuit%201%20(470R).gif)
![circuit 2 (220R).gif](/img/user/circuit%202%20(220R).gif)