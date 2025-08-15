# OIBSIP
Created a number guessing game using java programming 

 import javax.swing.JOptionPane;
import java.util.Random;

public class NumberGuessingGame {
    public static void main(String[] args) {
        Random random = new Random();
        int targetNumber = random.nextInt(200) + 1; // Random number between 1 and 200
        int guess;
        int attempts = 0;
        int score = 0;
        boolean correct = false;

        JOptionPane.showMessageDialog(null, "Welcome to the Number Guessing Game!\nI'm thinking of a number between 1 and 200. Try to guess it!");

        while (!correct) {
            String input = JOptionPane.showInputDialog("Enter your guess (1 to 200):");

            if (input == null) {
                // User clicked cancel or closed the dialog
                JOptionPane.showMessageDialog(null, "Game cancelled. Goodbye!");
                return;
            }

            try {
                guess = Integer.parseInt(input);
                attempts++;

                if (guess < 1 || guess > 200) {
                    JOptionPane.showMessageDialog(null, "Please enter a number between 1 and 200.");
                    continue;
                }

                if (guess == targetNumber) {
                    correct = true;

                    // Scoring logic based on attempts
                    if (attempts <= 3) {
                        score = 100;
                    } else if (attempts <= 6) {
                        score = 75;
                    } else if (attempts <= 10) {
                        score = 50;
                    } else {
                        score = 25;
                    }

                    JOptionPane.showMessageDialog(null,
                        "🎉 Congratulations! You guessed the number in " + attempts + " attempt(s).\n" +
                        "Your score: " + score + " points.");
                } else if (guess < targetNumber) {
                    JOptionPane.showMessageDialog(null, "Too low! Try a higher number.");
                } else {
                    JOptionPane.showMessageDialog(null, "Too high! Try a lower number.");
                }
            } catch (NumberFormatException e) {
                JOptionPane.showMessageDialog(null, "Invalid input! Please enter a valid number.");
            }
        }

        // Optionally ask if the user wants to play again
        int playAgain = JOptionPane.showConfirmDialog(null, "Would you like to play again?", "Play Again", JOptionPane.YES_NO_OPTION);
        if (playAgain == JOptionPane.YES_OPTION) {
            main(null); // Restart the game
        } else {
            JOptionPane.showMessageDialog(null, "Thanks for playing! Goodbye.");
        }
    }
}
