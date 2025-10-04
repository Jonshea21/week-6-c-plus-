using System;

// This class encapsulates the grading logic, demonstrating better OOP principles.
public class GradeAnalyzer
{
    // Define the weights for each component
    private const double HomeworkWeight = 0.40; // 40%
    private const double MidtermWeight = 0.30;  // 30%
    private const double FinalWeight = 0.30;    // 30%

    // Method to calculate the final score and return the letter grade
    public string CalculateGrade(double homeworkScore, double midtermScore, double finalScore)
    {
        // ----------------------------------------------------
        // Example 1: Input Validation (Uses Logical OR ||)
        // Check if any score is outside the valid 0-100 range.
        // ----------------------------------------------------
        if (homeworkScore < 0 || homeworkScore > 100 || 
            midtermScore < 0 || midtermScore > 100 || 
            finalScore < 0 || finalScore > 100)
        {
            return "Error: All scores must be between 0 and 100.";
        }

        // Calculate the weighted final score
        double finalScoreWeighted = 
            (homeworkScore * HomeworkWeight) +
            (midtermScore * MidtermWeight) +
            (finalScore * FinalWeight);

        // Round the score for cleaner output
        finalScoreWeighted = Math.Round(finalScoreWeighted, 2);

        // Determine the letter grade using a robust if-else if structure
        string letterGrade;

        // ----------------------------------------------------
        // Example 2: Multi-criteria Decision Making (if-else if)
        // Note: The checks are ordered from highest to lowest score.
        // ----------------------------------------------------
        if (finalScoreWeighted >= 90)
        {
            letterGrade = "A";
        }
        else if (finalScoreWeighted >= 80)
        {
            letterGrade = "B";
        }
        else if (finalScoreWeighted >= 70)
        {
            letterGrade = "C";
        }
        else if (finalScoreWeighted >= 60)
        {
            letterGrade = "D";
        }
        else
        {
            // The final 'else' captures all scores below 60
            letterGrade = "F";
        }

        // Return a formatted result string
        return $"Final Score: {finalScoreWeighted}%\nLetter Grade: {letterGrade}";
    }

    // Method to handle user interaction and input
    public void RunInteractiveMode()
    {
        Console.WriteLine("--- Interactive Grade Calculator (40/30/30 Weights) ---");
        Console.WriteLine("Enter scores (0-100) for Homework (40%), Midterm (30%), and Final (30%).");
        
        try
        {
            // Get Homework Score
            Console.Write("Enter Homework Score (0-100): ");
            double homework = Convert.ToDouble(Console.ReadLine());

            // Get Midterm Score
            Console.Write("Enter Midterm Score (0-100): ");
            double midterm = Convert.ToDouble(Console.ReadLine());

            // Get Final Exam Score
            Console.Write("Enter Final Exam Score (0-100): ");
            double finalExam = Convert.ToDouble(Console.ReadLine());

            // Calculate and display the result
            string result = CalculateGrade(homework, midterm, finalExam);
            
            Console.WriteLine("\n--- Result ---");
            Console.WriteLine(result);
            Console.WriteLine("--------------");
        }
        catch (FormatException)
        {
            // Exception handling for non-numeric input (Robustness)
            Console.WriteLine("\nERROR: Invalid input. Please enter valid numbers only.");
        }
    }
}

// Main program entry point
class Program
{
    static void Main()
    {
        // Instantiating the GradeAnalyzer class (OOP principle)
        GradeAnalyzer analyzer = new GradeAnalyzer();
        analyzer.RunInteractiveMode();
        
        // Keep console open until a key is pressed
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
