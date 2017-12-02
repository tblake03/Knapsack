# Knapsack
GA or EVO Knapsack Problem


# create a library of nodes that we can use to build syntax trees. Deciding which functions and terminals to include is problem dependent

Library = gpLibrary()
for i in -10:10
    Library.addTerminal(i);
end


# add input variable as a terminal

library.addTerminal(X);
library.addFunction(+,2);
library.addFunction(-,2);
library.addFunction(/,2);
library.addFunction(*,2);
library.addTerminal(pi);
library.addFunction(sin,1);
library.addfunction(cos,1);

# define a fitness function to minimize(neasure of error). (Use RMSE)
fitFunct = function(treeOutput)
    sqrt(mean((treeOutput-Y).^2))
   end

# initialize a GP instance to run in serial w/ 50% mutation rate and a pop size of 200. We then run the GP for 1000 generations and look at the Pareto font 

serial_G = GP(library,fitFunct, vars=Dict("X"=>X, "pi"=>pi),islandCount=1,mutate=0.5, popSize=200);
@time serial_G.run(1000);

# 18.821 seconds (33.90 M allocations)
