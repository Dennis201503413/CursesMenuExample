As we discussed on our previous Curses tutorial which can be found here, a library that supplies a **terminal-independent screen-painting and keyboard-handling facility for text based terminals**, we already showed how the library works painting a moving dot on the screen, but now we will use it to our advantage to develop a Menu for our curses application, in this case we will be building a “Snake game”, so the Menu will work accordingly.

We will start by defining a few **methods** that will help us to cycle thru our Menus with ease, and also will help our code to look *neat* and *organized*.

### paint_title()

Since we will be navigating to many options in our application, it’s important to define a new title every time we have a different functionality in the screen.

``` python
def paint_title(win,var):
    win.clear()                         #it's important to clear the screen because of new functionality everytime we call this function
    win.border(0)                       #after clearing the screen we need to repaint the border to keep track of our working area
    x_start = round((60-len(var))/2)    #center the new title to be painted
    win.addstr(0,x_start,var)           #paint the title on the screen
```

### paint menu()

This methods receives a curses window, since everything we will be painting will be painted on this window, first we paint a title with the **paint_title()** method we built, also we define our window timeout to **-1** (*making sure it waits until an input is received*).

``` python
def paint_menu(win):
    paint_title(win,' MAIN MENU ')          #paint title
    win.addstr(7,21, '1. Play')             #paint option 1
    win.addstr(8,21, '2. Scoreboard')       #paint option 2
    win.addstr(9,21, '3. User Selection')   #paint option 3
    win.addstr(10,21, '4. Reports')         #paint option 4
    win.addstr(11,21, '5. Bulk Loading')    #paint option 5
    win.addstr(12,21, '6. Exit')            #paint option 6
    win.timeout(-1)                         #wait for an input thru the getch() function
```

### wait_esc()

our **wait_esc()** function is a simple function that will wait for the **[ESC]** key to be pressed.

``` python
def wait_esc(win):
    key = window.getch()
    while key!=27:
        key = window.getch()
```

## Core Application

Now we will start building our core application, since we are building a curses application we will borrow most of the configurations already explained in the last tutorial and as the first thing the user will see will be the Menu, we will also paint it as follows:

``` python
stdscr = curses.initscr() #initialize console
window = curses.newwin(20,60,0,0) #create a new curses window
window.keypad(True)     #enable Keypad mode
curses.noecho()         #prevent input from displaying in the screen
curses.curs_set(0)      #cursor invisible (0)
paint_menu(window)      #paint menu
```

### Functional Menu

Finally we will have **simulated switch statement** thru an **if-elif-else** sentence, and will run this statement as long as the exit option (6) is not pressed, since curses uses **ASCII** for keys and we will be using number *1-6*, the ascii equivalents will be *49-54*, every time we enter an option we will paint the option title on the screen and call our **wait_esc()** method, that will wait for **[ESC]** to be pressed and then we will return to the Main Menu by painting it and defining our keystroke to -1.

``` python
keystroke = -1
while(keystroke==-1):
    keystroke = window.getch()  #get current key being pressed
    if(keystroke==49): #1
        paint_title(window, ' PLAY ')
        wait_esc(window)
        paint_menu(window)
        keystroke=-1
    elif(keystroke==50):
        paint_title(window, ' SCOREBOARD ')
        wait_esc(window)
        paint_menu(window)
        keystroke=-1
    elif(keystroke==51):
        paint_title(window, ' USER SELECTION ')
        wait_esc(window)
        paint_menu(window)
        keystroke=-1
    elif(keystroke==52):
        paint_title(window, ' REPORTS ')
        wait_esc(window)
        paint_menu(window)
        keystroke=-1
    elif(keystroke==53):
        paint_title(window,' BULK LOADING ')
        wait_esc(window)
        paint_menu(window)
        keystroke=-1
    elif(keystroke==54):
        pass
    else:
        keystroke=-1
```
