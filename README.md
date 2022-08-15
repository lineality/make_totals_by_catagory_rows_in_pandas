# make_totals_by_catagory_rows_in_pandas
```
"""
Totals by type:
Sometime you will have a dataframe where each row is some item, 
but you need a dataset where each catagory is a row with totals as columns
in that catagory.

Here is working code to do that (on the fly) in python. 

Create a new dataframe in which the rows are states 
and there is a column for total values.

e.g. total number of EV charging stations per state

"""

import pandas as pd

# open original df
df = pd.read_csv("US_Alt_Fuel_Stations_03_17_2022.csv")

# make a list of states
list_of_states = df["State"].unique()

# create new blank df_states
df_states = pd.DataFrame()

# iterate through list of states
for i in list_of_states:
    # get name (initials) of state
    state_two_letters = i

    # get number of ev stations in that state
    number_of_ev_stations_per_state = df[ (df["State"] == state_two_letters) & (df["Status Code"] == "E") ].shape[0]

    # make new row
    df_states = df_states.append({'State':i}, ignore_index=True)

    ### Alternate Method
    # # Inserting a Row at a Specific Index
    # df.loc[len(df)] = ['Jane', 25, 'Madrid']

    # update/ change row label to be the same a certain 
    df_states.index = df_states["State"]

    # save those data
    df_states.loc[state_two_letters, "ev_count_per_state"] = number_of_ev_stations_per_state


# save csv
df_states.to_csv('states_ev.csv', index=False) 

# print header)
print( df_states.head(5) )
```
