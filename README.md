# Complex-System-530
import turtle
import random

ant1 = turtle.Turtle
ant2 = turtle.Turtle


def main():
    
    ant1.setup (2000,2000,0,0)
    ant2.setup (2000,2000,0,0)
    ant1.speed (-1)
    ant2.speed (-1)
    ant1.penup()
    ant2.penup()
    ant1.right(180)
    ant2.left(180)


def position1(ant1):
    return (round(ant1.xcor()), round(ant1.ycor()))

def position2(ant2):
    return (round(ant2.xcor()), round(ant2.ycor()))
    
 # define a set of colors so that besides initial colors of the ants' places,random colors are generated during ants' movements
COLORS = COLORS = ["blue", "black", "red", "yellow", "green", "orange"]

def pick_color(colors=[], previous=[None]):
    if not colors:
        colors.extend(COLORS)
        random.shuffle(colors)
        if colors[-1] == previous[0]:
            colors.insert(0, colors.pop())
    previous[0] = colors.pop()

    return previous[0]

def update_maps(graph, ant1, ant2, color):
    graph[position1,position2] = color
    return None

def move1(ant1, pos1,maps, step): #white color to begin with and can change to any other color in the range
    if position1 not in maps or maps[position1] == "white":
        random_color = pick_color()
        ant1.fillcolor(random_color)
        ant1.stamp()
        update_maps(maps, ant1, random_color)
        ant1.right(90)
        ant1.forward(step)
        pos1 = position1(ant1)
        
    elif maps[pos1] == "black":
        random_color = pick_color()
        ant1.fillcolor(random_color)
        ant1.stamp()
        update_maps(maps, ant1, random_color)
        ant1.left(90)
        ant1.forward(step)
        pos1 = position1(ant1)
    return pos1

def move2(ant2, pos2, maps, step): #black color to begin with and can change to any other color
    if position2 not in maps or maps[position2] == "white":
        random_color = pick_color()
        ant2.fillcolor(random_color)
        ant2.stamp()
        update_maps(maps, ant2, random_color)
        ant2.left(90)
        ant2.backward(step)
        pos2 = position2(ant2)
        
    elif maps[pos2] == "black":
        random_color = pick_color()
        ant2.fillcolor(random_color)
        ant2.stamp()
        update_maps(maps,ant2, random_color)
        ant2.right(90)
        ant2.backward(step)
        pos2 = position2(ant2)
    return pos2


def Run():
    BACKGROUND_COLOR = "white"

    #shape of ant
    SHAPE = "square"
    SIZE = 0.3
    STEP = 11
    maps = {}

    window = turtle.Screen()
    window.bgcolor(BACKGROUND_COLOR)

    # Initialize Ant
    ant1.shape(SHAPE)
    ant2.shape(SHAPE)
    ant1.shapesize(SIZE)
    ant2.shapesize(SIZE)
    ant1.penup()
    ant2.penup()
    ant1.right(180)
    ant2.left(180)
    pos1 = position1(ant1)
    pos2 = position2(ant2)

    moves = 0
    while True:
        pos1 = move1(ant1, pos1, maps, STEP)
        pos2 = move2(ant2, pos2, maps, STEP)
        moves += 1
        print ("Movements:", moves)

Run()
