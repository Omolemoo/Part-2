# Part-2

 Here are the instructions to compile and run the software:

Install Visual Studio: If you haven't already, download and install Visual Studio from the official Microsoft website. Ensure you have the required .NET development workload installed.

Create a New Console Application Project: Open Visual Studio and create a new C# Console Application project. Name it "RecipeApp" or any other preferred name.

Create a c#Code

Review and Modify Code (Optional): Review the code to ensure it meets your requirements. You can make modifications if necessary.

Save Changes: Save the changes made to the Program.cs file.

Compile the Project: Click on the "Build" menu at the top of Visual Studio, then select "Build Solution" to compile the project. Ensure there are no compilation errors.

Run the Application: Once the compilation is successful, you can run the application by clicking on the "run" button in Visual Studio or by pressing Ctrl + F5.
using System;

namespace RecipeApp
{
    // Class to represent an Ingredient with name, quantity, unit, calories, and food group
    class Ingredient
    {
        public string Name { get; set; }
        public double Quantity { get; set; }
        public string Unit { get; set; }
        public double Calories { get; set; }
        public string FoodGroup { get; set; }
    }

    // Class to represent a Recipe with name, ingredients, and steps
    class Recipe
    {
        public string Name { get; set; }
        public List<Ingredient> Ingredients { get; set; }
        public List<string> Steps { get; set; }

        public Recipe(string name)
        {
            Name = name;
            Ingredients = new List<Ingredient>();
            Steps = new List<string>();
        }

        public double CalculateTotalCalories()
        {
            double totalCalories = 0;
            foreach (var ingredient in Ingredients)
            {
                totalCalories += ingredient.Calories;
            }
            return totalCalories;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Create a list to store recipes
            List<Recipe> recipes = new List<Recipe>();

            // Enter and manage the recipes
            EnterRecipes(recipes);

            // Display all the recipes
            DisplayAllRecipes(recipes);
        }

        static void EnterRecipes(List<Recipe> recipes)
        {
            while (true)
            {
                // Get recipe name from user
                Console.Write("Enter recipe name (or 'done' to finish entering recipes): ");
                string recipeName = Console.ReadLine();
                if (recipeName.ToLower() == "done")
                    break;

                // Create new recipe object
                Recipe recipe = new Recipe(recipeName);

                // Enter ingredients for the recipe
                Console.WriteLine($"Enter ingredients for recipe '{recipeName}':");
                while (true)
                {
                    // Get ingredient details from user
                    Console.Write("Ingredient name: ");
                    string ingredientName = Console.ReadLine();
                    if (string.IsNullOrWhiteSpace(ingredientName))
                        break;
                    
                    Console.Write("Quantity: ");
                    double quantity = double.Parse(Console.ReadLine());

                    Console.Write("Unit: ");
                    string unit = Console.ReadLine();

                    Console.Write("Calories: ");
                    double calories = double.Parse(Console.ReadLine());

                    Console.Write("Food group: ");
                    string foodGroup = Console.ReadLine();

                    // Create new ingredient object and add it to the recipe
                    Ingredient ingredient = new Ingredient
                    {
                        Name = ingredientName,
                        Quantity = quantity,
                        Unit = unit,
                        Calories = calories,
                        FoodGroup = foodGroup
                    };
                    recipe.Ingredients.Add(ingredient);
                }

                // Enter steps for the recipe
                Console.WriteLine($"Enter steps for recipe '{recipeName}':");
                while (true)
                {
                    // Get step details from user
                    Console.Write("Step: ");
                    string step = Console.ReadLine();
                    if (string.IsNullOrWhiteSpace(step))
                        break;

                    // Add step to the recipe
                    recipe.Steps.Add(step);
                }

                // Add the recipe to the list of recipes
                recipes.Add(recipe);
                Console.WriteLine($"Recipe '{recipeName}' added successfully!\n");
            }
        }

        static void DisplayAllRecipes(List<Recipe> recipes)
        {
            Console.WriteLine("All Recipes:");
            foreach (var recipe in recipes)
            {
                Console.WriteLine($"- {recipe.Name}");
                Console.WriteLine($"Total Calories: {recipe.CalculateTotalCalories()}");

                // Check if total calories of the recipe exceed 300 and notify the user
                if (recipe.CalculateTotalCalories() > 300)
                {
                    Console.WriteLine("Warning: Total calories exceed 300!");
                }
            }
        }
    }
}
