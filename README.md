# TwentyQuestions
/**
 This is an off shoot of the game twenty questions
 @creator Yanni Angelides
 @version 01/5/16
 */
 
import java.io.*;
import java.util.Scanner;
import java.lang.String;
 
 public class TwentyQuestions
 {
 	public static BinaryTree<String> tree = new BinaryTree<String>("Is it an Apple?"); //set to the first question in the game
 	
 	/**
 	Plays one cycle of the 20 questions game.  
 	@param BinaryTree within the larger BinaryTree that the method should start at
 	@return boolean indicating whether or not the program should run again. (Determines the value of the run variable in the main method)
 	*/
 	public static boolean gameCycle(BinaryTree<String> b)
 	{
 		Scanner input = new Scanner(System.in);
 		System.out.println(b.value());
 		if(input.nextLine().equals("yes"))
 		{
 			if(b.isLeaf()) //means that the player has reached an item and the program should guess 
 			{
 				System.out.print("You Win"); //if the guess is right the program wins
 				return false;
 			}
 			else
 			{
 				gameCycle(b.right()); //moves to the next question on the right side of the tree
 			}		
 		}
 		else
 		{
 			if(b.isLeaf())
 			{
 				b.setLeft(new BinaryTree<String>(b.value())); //need to create a new binary tree because at the moment the space is null
 				System.out.println("Type in a question."); 
 				b.setValue(input.nextLine()); //sets the value of the new BinaryTree to the question the user inputs
 				System.out.println("What was you object");
 				b.setRight(new BinaryTree<String>("Is it a(n) " + input.nextLine())); //sets the right side of the BinaryTree to the object the user was thinking of
 				System.out.println("Do you want to play again?");
 				if(input.nextLine().equals("yes"))
 				{
 					return true;	
 				}
 				else
 				{
 					return false;
 				}
 			}
 		}
 		return true;
 	}
	
	public static void main(String [] args)
	{
		System.out.println("Welcome to 20 Questions! Please think of an object.");
		boolean run = true;
		while (run == true) //Loop to make the game keep going
		{
			if(gameCycle(tree) == true)
			{
				gameCycle(tree); //Starts the game	
			}
			else
			{
				run = false;
			}
		}
	}
 }
