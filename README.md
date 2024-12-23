# Pong Game in C# with Windows Forms



https://github.com/user-attachments/assets/88da60e5-e434-4916-8412-fa5397ba2b86



This project is a simple implementation of the classic Pong game in C# using Windows Forms in Visual Studio.


## Getting Started


### Installation

1. Clone or download this repository.
2. Open the project in Visual Studio.
3. Build and run the application.

## Code 
```csharp

namespace PONG
    

{
   
    public partial class Pong : Form

    {

        // Location Variables

        int cpuDirection = 30; // set speed for cpu move up and down in screen

        int ballXCoordinate = 30; // set ball speed as well

        int ballYCoordinate = 30;

        // Score Variables

        int playerScore = 0; 

        int cpuScore = 0;

        // Size Variables

        int bottomBoundary; // the paddle cant go past the bottom of the sreen , if happen,stop

        int centerPoint;

        int xMidpoint; //to calc the center point

        int yMidpoint;

        // Detection Variables

        bool playerDetectedUp; //plater up or down

        bool playerDetectedDown;

        // Special Keys

        int spaceBarClicked = 0; // puse game 

     
        


        public Pong()

        {

            InitializeComponent();

            bottomBoundary = ClientSize.Height - player1.Height; // get size of window  - height of paddle

            xMidpoint = ClientSize.Width / 2; // width of the window / 2 , to be in the center 

            yMidpoint = ClientSize.Height / 2; // width of the window / 2 , to be in the center

        }



        private void pongTimer_Tick(object sender, EventArgs e)

        {
        
            
            Random newBallSpot = new Random(); 

            int newSpot = newBallSpot.Next(100, ClientSize.Height - 100); // random number to range the ball

            // Adjust where the ball is

            pongBall.Top -= ballYCoordinate; // top of picturebox = top of picturebox - ballYCoordinate 30 down

            pongBall.Left -= ballXCoordinate;

            // Make the CPU move

            cpuPlayer.Top += cpuDirection; //Move up



            if (playerScore > 2)

            {

                cpuPlayer.Top = pongBall.Top + 40;

            }

            // Check if CPU has reached the top or the bottom

            if (cpuPlayer.Top < 0 || cpuPlayer.Top > bottomBoundary)  // 0 is top of screen
            {
                cpuDirection = -cpuDirection; // back down //-30
            }

            // Check if the ball has exited the left side of the screen

            if (pongBall.Left < 0 ) // pass screen boundry

            {

                pongBall.Left = xMidpoint;

                pongBall.Top = newSpot; // random number to the hight

                ballXCoordinate = -ballXCoordinate; 

                if (playerScore < 2) { ballXCoordinate -= 1; }

                cpuScore++;

                cpuScoreLabel.Text = cpuScore.ToString();

            }



            // Check if the ball has exited the right side of the screen

            if (pongBall.Left + pongBall.Width > ClientSize.Width)

            {

                pongBall.Left = xMidpoint;

                pongBall.Top = newSpot;

                ballXCoordinate = -ballXCoordinate; // move -30 for other direction

                if (playerScore < 2) { ballXCoordinate += 2; }

                playerScore++;

                playerScoreLabel.Text = playerScore.ToString();
                cpuScoreLabel.Text = cpuScore.ToString();



            }

            // Ensure the ball is within the boundaries of the screen

            if (pongBall.Top < 0 || pongBall.Top + pongBall.Height > ClientSize.Height) { ballYCoordinate = -ballYCoordinate; }



            // Check if the ball hits the player or CPU paddle

            if (pongBall.Bounds.IntersectsWith(player1.Bounds) || pongBall.Bounds.IntersectsWith(cpuPlayer.Bounds))

            {

                // Send ball opposite direction

                ballXCoordinate = -ballXCoordinate; 

            }

            // Move player up

            if (playerDetectedUp == true && player1.Top > 0) { player1.Top -= 100; }

            // Move player down

            if (playerDetectedDown == true && player1.Top < bottomBoundary) { player1.Top += 100; }

            // Check for winner

            if (playerScore >= 10)
            {
                pongTimer.Stop();
                string message = " YOU WON!!";
                string title = "WINNER OF THE GAME";
                MessageBox.Show(message, title);

            }
            else if (cpuScore >= 10)
            {
                pongTimer.Stop();
                string message = " CPU WON!!";
                string title = "WINNER OF THE GAME";
                MessageBox.Show(message, title);

            }

        }



        private void Pong_KeyUp(object sender, KeyEventArgs e)

        {

            if (e.KeyCode == Keys.Up) { playerDetectedUp = false; }

            if (e.KeyCode == Keys.Down) { playerDetectedDown = false; }



        }



        private void Pong_KeyDown(object sender, KeyEventArgs e) 

        {

            // If player presses the up arrow, move paddle upwards

            if (e.KeyCode == Keys.Up) { playerDetectedUp = true; }

            // If player presses the down arrow, move paddle downwards

            if (e.KeyCode == Keys.Down) { playerDetectedDown = true; }



            // If player presses space bar, pause the game

            if (e.KeyCode == Keys.Space)

            {

                if (spaceBarClicked % 2 == 0)

                {

                    pongTimer.Stop();

                }

                else

                {

                    pongTimer.Start();

                }

            }

            spaceBarClicked++;

        }

        private void pongBall_Click(object sender, EventArgs e)
        {

        }

        private void cpuPlayer_Click(object sender, EventArgs e)
        {

        }

        private void playerScoreLabel_Click(object sender, EventArgs e)
        {

        }

        private void Pong_Load(object sender, EventArgs e)
        {

        }

        private void pictureBox2_Click(object sender, EventArgs e)
        {

        }
    }
}
```
## How to Play

- Use the arrow keys to control the paddle and hit the ball.
- The objective is to prevent the ball from passing your paddle while trying to bounce it back towards the opponent's side.
- Score points by making the ball pass your opponent's paddle.

## Authors

- [Shatha Altassan]
- [Afrah Alharbi]

