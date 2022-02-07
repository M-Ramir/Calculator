# Calculator
// Calc - Creates A working calculator ( To be used with CalculatorGUI). Calculator does simple calculations such as addition
// subtraction, multiplication, and division. Numbers can be single digit or double digit with or without decimal.
// Calculator has option to clear entry, clear, or backspace depending on button used.
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Calc
{
    public partial class Form1 : Form

    {   
        // All variables set to be used in later code
        // Sets string to an empty string
        private string mathOperation = string.Empty;
        // Sets double to 0.0 
        private double leftOperand = 0.0;
        // Sets boolean to false 
        private bool beginningMathOp = false;

        public Form1()
        {
            InitializeComponent();
        }
        
        // Clears all other entries
        private void clearBtn_Click(object sender, EventArgs e)
        {
            display.Clear();
        }
        private void numBtn_Click(object sender, EventArgs e)
        {

            // If button is clicked displays each number, one ater the other
            // Numbers clear after each operation is used and displays answer
            if (display.Text == "0" || beginningMathOp == true && display.Text != ".")
            {
                display.Clear();
            }

            beginningMathOp = false;
            display.Text += ((Button) sender).Text;
        }

        // Displays zero when clear entry button is clicked
        private void clearEntryBtn_Click(object sender, EventArgs e)
        {
            display.Text = "0";
        }

        // Checks if the display text contains a dot
        // If dot is already added doesn't display additional dots
        // If display doesn't contain a dot, new dot is placed in display
        private void decimalBtn_Click(object sender, EventArgs e)
        {
            
           display.Text = (display.Text.Contains(".")) ? display.Text : display.Text + ".";
           
        }
        private void equalsBtn_Click(object sender, EventArgs e)
        {
            // Checks which math operations are used 
            switch(mathOperation)
            {   
                // if + is used leftOperand adds next button clicked and displays
                case"+":
                    display.Text = (leftOperand + double.Parse(display.Text)).ToString();
                    break;
                // if - is used leftOperand subtracts next button clicked and displays
                case "-":
                    display.Text = (leftOperand - double.Parse(display.Text)).ToString();
                    break;
                // if x is used leftOperand muliplies next button clicked and displays
                case "x":
                    display.Text = (leftOperand * double.Parse(display.Text)).ToString();
                    break;
                //// if / is used leftOperand divides next button clicked and displays
                case "/":
                    display.Text = (leftOperand / double.Parse(display.Text)).ToString();
                    break;
                default:
                    // if code gets passed Error is written out
                    Console.WriteLine("ERROR!!");
                    break;
            }

        }
        // Starts a new math operation
        // Captures the math operation
        // Saves math operations
        private void mathOpBtn_Click(object sender, EventArgs e)
        {
            beginningMathOp = true;

            leftOperand = double.Parse(display.Text);

            mathOperation = ((Button)sender).Text;

        
        }
        // When button is clicked changes positive to negative
        // if number is negative and button is clicked changes it back to positive
        private void posNegBtn_Click(object sender, EventArgs e)
        {
            display.Text = (-double.Parse(display.Text)).ToString();
        }

        private void backBtn_Click(object sender, EventArgs e)
        {
            // if the string isn't empty and button is clicked one number is taken off at a time
            if(display.Text != String.Empty)

            {
                int displayLength = display.Text.Length;
                // Takes length of display text and takes one digit off each time 
                display.Text = display.Text.Remove(displayLength - 1);

            }
            else
            {   // if the string is empty nothing happens 
                display.Text = 0.ToString();
            }
    
            
              
        }
    }
}
