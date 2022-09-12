# Ping-Pong-Clone
import turtle

wd=turtle.Screen()
wd.bgcolor("blue")
wd.title("BLAH")
wd.setup(width=800, height=600)
wd.tracer()#stops window from updating, user does it manually

score_a=0
score_b=0

#scoring pen
pen=turtle.Turtle()
pen.speed(0)
pen.penup()
pen.write("Player A:0 Player B;0",align="center", font=("Fantabular", 18, 'italic'))


#paddle A
p_A=turtle.Turtle()
p_A.speed(0) #speed of paddle aka the animation. Not really. Still necessary 
p_A.color("red")
p_A.shape(name="square") #p_A.shape("rectangle")
p_A.shapesize(stretch_wid=5, stretch_len=1)
p_A.penup()
p_A.goto(-350, 0)

#paddle B
p_B=turtle.Turtle()
p_B.speed(0) #speed of paddle aka the animation. Not really. Still necessary 
p_B.color("red")
p_B.shape(name="square") #p_A.shape("rectangle")
p_B.shapesize(stretch_wid=5, stretch_len=1)
p_B.penup()
p_B.goto(350, 0)

#ball
ball=turtle.Turtle()
ball.speed(0) #speed of paddle aka the animation. Not really. Still necessary 
ball.color("green")
ball.shape(name="circle") #p_A.shape("rectangle")
ball.goto(0, 0)
ball.penup()
ball.dx=4
ball.dy=-4

#functions 
def p_A_up():
    y=p_A.ycor() #returns y coordinate
    y+=20
    p_A.sety(y)# set value of paddle to new y 

def p_A_down():
    y=p_A.ycor() #cause it's basically going up and down. Vertically. Returning y coordinate of object p_A
    y-=20
    p_A.sety(y)

def p_B_up():
    y=p_B.ycor() #returns y coordinate
    y+=20
    p_B.sety(y)

def p_B_down():
    y=p_B.ycor() #returns y coordinate
    y-=20
    p_B.sety(y)

#keyboard binding
wd.listen()#listen for keyboard input
wd.onkeypress(p_A_up, "w")
wd.onkeypress(p_A_down, "s")
wd.onkeypress(p_B_up, "Up")
wd.onkeypress(p_B_down, "Down")

#main game loop
while True:
    wd.update()  #updates screen everytime code runs(w/o it screen falls away)

    #moving the ball
    ball.setx(ball.dx + ball.xcor())#setting x coordinate, ball.dx is changing x coordinate
    ball.sety(ball.dy + ball.ycor())

    #border checking
    if ball.ycor()>290:
        ball.sety(290)
        ball.dy*=-1#reverses direction 

    if ball.ycor()<-290:
        ball.sety(-290)
        ball.dy*=-1

    if ball.xcor()>390:
        ball.goto(0,0)
        ball.dx*=-1
        score_a+=1
        pen.clear()
        pen.write("Player A:{} Player B:{}".format(score_a, score_b),align="center", font=("Fantabular", 18, 'italic'))
    

    if ball.xcor()<-390:
        ball.goto(0,0)
        ball.dx*=-1
        score_b+=1
        pen.clear()
        pen.write("Player A:{} Player B:{}".format(score_a, score_b),align="center", font=("Fantabular", 18, 'italic'))
        

    #p and ball meet
    if (ball.xcor() > 340 and ball.xcor()<350)  and (ball.ycor()<p_B.ycor()+40 and ball.ycor()>p_B.ycor()-40):
        ball.setx(340)
        ball.dx*=-1

    if (ball.xcor() < -340 and ball.xcor()>-350)  and (ball.ycor()<p_A.ycor()+40 and ball.ycor()>p_A.ycor()-40):#fool
        ball.setx(-340)
        ball.dx*=-1

    
