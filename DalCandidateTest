import pandas
from matplotlib import pyplot


class State:
    """
    A state represents each state in brazil

    Attributes
    ----------
    name: str
        holds the name of the state
    years: {}
        dictionary holding key value pairs of {year fire occured: how many occured}

    Methods
    -------
    printyears() -> str
        returns the years fires occurred in a state
    printfires()
        return the total fires of a state
    """

    def __init__(self, name):
        """
        Parameters
        ----------
        :param name: str
           name of the state
        """
        self.name = name
        self.years = {}

    def __str__(self):
        return self.name + " " + str(self.fires) + " " + str(([str(year) for year in self.years]))

    def printyears(self):
        """
        :return: str
            string of years separated by commas
        """
        return_string = ""
        for year, value in self.years.items():
            if value >= 0:
                return_string += str(year) + ", "
        return return_string

    def printfires(self):
        """
           :return: int
               number of fires
        """
        fires =0
        for number in self.years.values():
            fires += number
        return int(fires)


""" Task 1 (20 minutes)
This section  extracts the relevant data from the csv file and creates States   
"""
csv = pandas.read_csv("C:/Users/Liam/Downloads/amazon.csv", usecols=[0, 1, 2, 3], encoding='latin1')
stateList = list()
found = False
for index, row in csv.iterrows():
    for state in stateList:
        if state.name != row['state']:
            found = False
        else:
            found = True
            stateName = state
            break
    if not found:
        stateName = State(row['state'])
        stateList.append(stateName)
    if str(row['year']) not in stateName.years:
        stateName.years[str(row['year'])] = row['number']
    else:
        stateName.years[str(row['year'])] += row['number']


""" Task 1.1 (10 minutes)
Loops through previously created list of states and prints their name and uses their printfires()/printyears() methods
"""

print("Task One:\n")
for State in stateList:
    print(State.name + ", " + str(State.printfires()) + " times, in the years " + str(State.printyears()))
print()

""" 
Task 1.2 (30 minutes) & Task 1.3 (10 minutes)
1.2 -> How many fires occurred in each year and in what states
1.3 -> Year with the most fires and which state had the most fires in that year
"""

print("Task 1.2 \n")
sortedYears = sorted(state.years.items())
mostFires = 0
yearWithMostFires = str(sortedYears[0][0])
for year in range(0, stateList[0].years.__len__()):
    total = 0
    includedStates = ''
    for state in stateList:
        total += state.years[sortedYears[year][0]]
        if state.years[sortedYears[year][0]] >= 0:
            includedStates += (state.name + ", ")
    if total > mostFires:
        mostFires = total
        yearWithMostFires = int(sortedYears[year][0])
    print("In " + str(int(sortedYears[year][0])) + ", " + str(int(total)) + " times, in states " + includedStates)
stateWithMostFire = ''
tempFires = 0
for state in stateList:
    if state.years[str(yearWithMostFires)] > tempFires:
        tempFires = state.years[str(yearWithMostFires)]
        stateWithMostFire = state.name
print("\nTask 1.3 \n")
print("There were " + str(int(mostFires)) + " Forest Fires in " + str(yearWithMostFires) +
      ". That year, the most Forest Fires occurred in " + stateWithMostFire + ".")
print("\n\n")


"""Task 1.4 (1 hour)
Collects year and forest fires from csv and plots the mean and std per year on the same graph
"""

data = pandas.read_csv("C:/Users/Liam/Downloads/amazon.csv", usecols=[0, 3], encoding='latin1')
mean_per_year = data.groupby('year').agg('mean')
std_per_year = data.groupby('year').std()
pyplot.plot(std_per_year, label='Std')
pyplot.plot(mean_per_year, label='Mean')
pyplot.legend()
pyplot.title("Mean")
pyplot.xlabel("Year")
pyplot.ylabel("Forest Fires")
pyplot.show()
