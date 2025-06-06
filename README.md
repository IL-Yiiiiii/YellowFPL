# YellowFPL

from itertools import repeat
import requests
import pandas as pd


url = "https://fantasy.premierleague.com/api/bootstrap-static/"
data = requests.get(url).json()
players_df = pd.DataFrame(data['elements'])  # Player stats
teams_df = pd.DataFrame(data['teams'])       # Team info


print("")
print("\033[1m" + "YellowFPL" + "\033[0m")
print("")
print("\033[4m" + "Available Options:" + "\033[0m")
print("0: Dip")
print("1: Search Players")
print("")
choice = int(input("What would you like to do: "))


if choice == 0:
   print("Ok Bye!")


if choice == 1:
   name = str(input("Type in player: "))
   for i in range(804):
       ppg = float(players_df["points_per_game"][i])
       player = str(players_df["web_name"][i])
       price = float(players_df["now_cost"][i] / 10)
       position_id = int(players_df["element_type"][i])
       team_id = int(players_df["team"][i])
       g_a = int(players_df["goals_scored"][i]) + int(players_df["assists"][i])
       goals = int(players_df["goals_scored"][i])
       assists = int(players_df["assists"][i])
       form = float(players_df["form"][i])
       first_name = str(players_df["first_name"][i])
       last_name = str(players_df["second_name"][i])
       full_name = str(players_df["first_name"][i] + " " + players_df["second_name"][i])
       number90s = float(round(players_df["minutes"][i] / 90, 2))
       starts = int(players_df["starts"][i])
       xG = float(players_df["expected_goals"][i])
       xA = float(players_df["expected_assists"][i])


       if position_id == 1:
           position = "Goalkeeper"
       elif position_id == 2:
           position = "Defender"
       elif position_id == 3:
           position = "Midfielder"
       elif position_id == 4:
           position = "Forward"
       elif position_id == 5:
           position = "Manager"


       team = str(teams_df["name"][team_id - 1])
       if player == name or first_name == name or last_name == name or full_name == name:
           print("Player", i)
           print("")
           print("\033[4m" + "Basic Info:" + "\033[0m")
           print("Full name:", full_name)
           print("Team:", team)
           print("Position:", position)
           print("")
           print("\033[4m" + "FPL indicators:" + "\033[0m")
           print("Price:", price)
           print("Points per game:", ppg)
           print("Form:", form)
           print("")
           print("\033[4m" + "Football stats:" + "\033[0m" + "")
           print("Starts:", starts)
           print("Number of 90s completed:", number90s)
           print("G/A:", g_a)
           print("Goals:", goals)
           print("xG:", xG)
           print("Assists:", assists)
           print("xA:", xA)
           print("")


