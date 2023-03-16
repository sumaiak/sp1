# sp1
projectBall


//intializing 
ArrayList<Ball> balls = new ArrayList<Ball>();
Ball b = new Ball();
Rectangle r = new Rectangle();


void setup() {
  size(600, 600);
  frameRate(100);
}

void draw() {
  background(255); 
  //for lines that intersect with each other
  for (int x = 0; x < width; x += 15) {
    stroke(255, 255, 0);
    line(x, 0, x, height);
  }
  for (int y = 0; y < height; y += 15) {
    stroke(255, 0, 0);
    line(0, y, width, y);
  }

  //calling different  functions for displaying the additional balls 
  b.displayBall();
  b.moveball();
  b.edges();
  r.displayRect();
  r.mousePressed();
  b.collision(r,balls);
  
//for colliding with the rect
  for (Ball ball : balls){
    ball.displayBall();
    ball.moveball();
    ball.edges();
    ball.collisionBall();
--------------------------------------------------------------------------------------------------------------------------------------------------------------------

class Ball {
//intializing and declaring instance variables
  public int x = 0;
  public int y = 0;
  float speedx = 4.5;
  float speedy = 2.5;
  color c;
  String s = "you lost";
  
  //for displaying ball
  public void displayBall() {
    fill(random(255), random(255), random(255));
    noStroke();
    ellipse(x, y, 50, 50);
  }

  void moveball() {
    x += speedx;
    y += speedy;
  }

  void edges() {
    if (x > width || 0 > x) {
      speedx = speedx * -1;
    }

    if (y > height) {
      // ball has touched bottom edge, make it disappear
      y = height + 70; // set y to a value outside the height of the window
    
    }

    if (y < 0) {
      speedy = speedy * -1;
    }
  }
  
void collision(Rectangle r, ArrayList<Ball> balls) {
   if (x + 25 > r.x - r.w/2 && 
      x - 25 < r.x + r.w/2 && 
       y + 25 > r.y - r.h/2 && 
       y - 25 < r.y + r.h/2) {
      speedx = -speedx;
      speedy = -speedy; 
      
      if (balls.size() <= 3) {
       balls.add(new Ball()); // adding a new ball to the list
             if(balls.size() < height+70){
      println("Game is over");
}
    
      }
       }
    


}
  
 void collisionBall(){
  if (x + 25 > r.x - r.w/2 && 
       x - 25 < r.x + r.w/2 && 
       y + 25 > r.y - r.h/2 && 
       y - 25 < r.y + r.h/2) {
      speedx = -speedx; // reverse direction of ball along x-axis
      speedy = -speedy;
 
       }
 
 }
}
-------------------------------------------------------------------------------------------------------------------------------------------------------------
class Rectangle {
  float x = 300;
  float y = 570;
  int  w =80;
  int h = 10;
  void displayRect() {
    rectMode(CENTER);
    fill(0, 255);
    rect(x, y, w, h);
  }

  void mousePressed() {
    //mouse right side of rect
    if (mouseX >x + 15) {
      x += 10;  // 
    }
    // mouse left side 
    else if (mouseX < x - 15) {
      x -= 10;  //
    }
  }
  
 
}

