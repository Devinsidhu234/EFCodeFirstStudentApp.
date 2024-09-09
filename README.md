// Student.cs
public class Student
{
    public int StudentId { get; set; }  // Primary Key
    public string Name { get; set; }    // Student Name
    public int Age { get; set; }        // Student Age
}
// SchoolContext.cs
using Microsoft.EntityFrameworkCore;

public class SchoolContext : DbContext
{
    public DbSet<Student> Students { get; set; }  // Represents the Students table

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        // Define the connection string to connect to the SQL Server database
        optionsBuilder.UseSqlServer(@"Server=(localdb)\mssqllocaldb;Database=StudentDB;Trusted_Connection=True;");
    }
}
// Program.cs
using System;

class Program
{
    static void Main(string[] args)
    {
        using (var context = new SchoolContext())
        {
            // Ensure the database is created based on the context model
            context.Database.EnsureCreated();

            // Create a new student object
            var student = new Student
            {
                Name = "Jane Doe",
                Age = 22
            };

            // Add the student to the Students DbSet
            context.Students.Add(student);

            // Save changes to the database
            context.SaveChanges();

            Console.WriteLine("Student added successfully!");
        }
    }
}
dotnet run
git init
git add .
git commit -m "Initial commit - EF Code-First Student App"
git remote add origin https://github.com/Devinsidhu234/EFCodeFirstStudentApp.git
git branch -M main
git push -u origin main

