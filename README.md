# Report of the project related to the course: “Programmazione per la Fisica”

Pierbattisti Goffredo, Colombo Giordano

# Introduction:
The code is an implementation of the SIR (Susceptible-Infectious-Recovered) model, a
mathematical model used to study the spread of infectious diseases in populations. The program
takes as input the probability of infection (beta), the probability of recovery (gamma), the duration
in days of the epidemic, and the number of susceptible, infected, and recovered individuals at the
beginning of the epidemic. It then outputs a complete day-by-day list of the evolution of the
numbers of susceptible, infected, and recovered individuals and a graphical representation of the
three variables.

# File structure:
The program consists of five files: "main.cpp", "sir_model.hpp", "sir_model.cpp", “sir_graph.hpp”
and “sir_graph.cpp”. The "main.cpp" file contains the main function, which initializes the model
object, checks the input, evolves the model, and outputs the results. The "sir_model.hpp" file
contains the definition of SIR struct and the SIRModel class while the "sir_model.cpp" file contains
the related implementation. The “sir_graph.hpp” contains the SIRGraph subclass definition based
on SIRModel and the “sir_graph.cpp” file contains the implementation of the added method.

# SIRModel:
The SIRModel class has four public methods: "check()", "dinamic()", "approx()", and "print()". The
"check()" method performs a consistency check on the types of the STDIN inserted parameters. The
"dinamic()" method calculates day by day the evolution of the values of S, I, and R and saves them
in the member vector "record_". The "approx()" method rounds the values of S, I, and R to
guarantee the constraint S + I + R = N. Finally, the "print()" method prints the results to standard
output.
The SIRModel class has four private member variables: "beta_", "gamma_", "days_", "N_", and
"record_". The "beta_" and "gamma_" variables represent the probability of infection and recovery,
respectively. The "days_" variable represents the duration of the epidemic. The "N_" variable
represents the total number of individuals in the population. The "record_" variable is a vector
where the values of S, I, and R will be saved during the model evolution.

# SIRGraph:
The "sir_graph.hpp" file defines the SIRGraph subclass of the SIRModel class. The SIRGraph class
add a single public method, "graph()", which generates a graphical representation of the evolution
of S, I, and R over time using the ROOT data analysis framework.
The creation of a subclass guarantees the independence of the code that makes use of the standard
C++ libraries from the one that uses the RootCern Framework, while maintaining the logical
coherence with the program architecture and ease of access to the data.
First, for each variable S, I, and R, a TGraph object is created, which is an object made up of two
arrays x and y with npoints each.
Next, a TCanvas object is allocated, which represents an area mapped to a window directly under
the control of the display manager. This object is divided into three pads, each containing a graph
for one of the three variables of the SIR model.Additionally, the titles of the x and y axes and the
color of the graph lines are set.
Finally, a point (x, y) is added for each day on which information about the SIR model has been
recorded, using the AddPoint method of the TGraph class.
The graph is then saved as a PNG image file, and all objects are deallocated to free up memory.

# Summary:
The "main.cpp" file creates an SIRGraph object, initializes it with the input values, checks the
input, evolves the model, generates the graphical representation, and prints the results to standard
output

# Copile string:
 g++ -Wall -Wextra -fsanitize=address  main.cpp -o main sir_model.cpp sir_graph.cpp `root-config --cflags --glibs`
