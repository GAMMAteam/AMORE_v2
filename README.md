- inputs to the algorithm
- various files needed to run the algorithm
- mechanism formatting
- settings
- conditions


The algorithm requires that the full mechanism be in the correct format. This format is a custom python based format which follows the following definition:
class Mechanism:
    def __init__(self, species, reactions):
        self.species = species
        self.reactions = reactions

class Reaction:
    def __init__(self, reactants, prod_dict, rate_law, eval_rate_law, rate, rate_string = '', multiplier = 1):
        self.reactants = reactants
        self.prod_dict = prod_dict
        self.rate_law = rate_law
        self.eval_rate_law = eval_rate_law
        self.rate = rate
        self.rate_string = rate_string
        self.multiplier = multiplier

A mechanism is an object class composed of a list of species and list of reactions. 
A reaction is an object class composed of:
- .reactants: a list of the reactants
- .prod_dict: a dictionary of the products with keys as the species and values as the stoichiometric coefficients
- .rate_law: a string of the rate law function
- .eval_rate_law: the evaluated rate law (optional)
- .rate: this is the relative rate and is as 1.
- .rate_string: this is left blank
- .multiplier: this is used in the algorithm but starts at one as the default

Regardless of the oiginal format of the full mechanism, it must be converted to this format. 
The notebooks for isoprene and camphene demonstrate this for two different initial mechanism file types.


Inputs to the algorithm:
- the mechanism in the above format
- conditions: a list of dictionaries (one dictionary for each condition) containing meteorological parameters and species concentrations needed to calculate the relative rates of each reaction
- background_species: a list of species that will default as secondary reactants when calculating relative rates, we usually use HOx, NOx, Ox species, and any other inorganic reactants or small organic radicals
- settings: a mix of optional and required settings for the reduction to proceed, listed below
