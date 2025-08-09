from logging import lastResort

import streamlit as st
import requests
import pandas as pd

url = "https://fantasy.premierleague.com/api/bootstrap-static/"
data = requests.get(url).json()
players_df = pd.DataFrame(data['elements']) # Player stats
teams_df = pd.DataFrame(data['teams'])       # Team info

# Sidebar for navigation
option = st.sidebar.selectbox("Menu", ["Home", "Search Players", "Compare Players", "Teams", "Experimentation"])
colour = st.sidebar.radio("Colour:", ["RED", "ORANGE", "GREEN", "BLUE", "PURPLE"])
if colour == "RED":
    st.title("***:red[YellowFPL]***")
elif colour == "ORANGE":
    st.title("***:orange[YellowFPL]***")
elif colour == "GREEN":
    st.title("***:green[YellowFPL]***")
elif colour == "BLUE":
    st.title("***:blue[YellowFPL]***")
elif colour == "PURPLE":
    st.title("***:violet[YellowFPL]***")
if option == "Home":
    st.write("Welcome to YellowFPL - Your Fantasy Premier League assistant!")
    st.write("Use the sidebar to navigate to different features.")
    if st.button("***:rainbow[Send balloons!]***"):
        st.balloons()
    colour = st.color_picker("Pick a color")
    st.write("---")
    st.slider("Pick a number", 0.0, 14.5, 0.1)

elif option == "Experimentation":
    st.header("*The dataframe*")
    st.dataframe(players_df)
    st.dataframe(teams_df)
    st.metric("HGA", 30, -10)

    st.write("Most objects")  # df, err, func, keras!
    st.write(["st", "is <", 3])
    st.write_stream(data)
    st.text("Fixed width text huh")
    st.markdown("_Markdown_")
    st.latex(r""" e^{i\pi} + 1 = 0 """)
    st.title("My title")
    st.header("My header")
    st.subheader("My sub")
    st.badge("New")
    st.html("<p>Hi!</p>")
    st.table(players_df.iloc[0:10])
    st.json({"foo": "bar", "fu": "ba"})

    # Two equal columns:
    col1, col2 = st.columns(2)
    col1.write("This is column 1")
    col2.write("This is column 2")

    # Three different columns:
    col1, col2, col3 = st.columns([3, 1, 1])
    # col1 is larger.

    # Bottom-aligned columns
    col1, col2 = st.columns(2, vertical_alignment="bottom")

    # You can also use "with" notation:
    with col1:
        st.radio("Select one:", [1, 2])

    st.context.cookies
    st.context.headers
    st.context.ip_address
    st.context.is_embedded
    st.context.locale
    st.context.theme.type
    st.context.timezone
    st.context.timezone_offset
    st.context.url

elif option == "Search Players":
    st.markdown("""
    <style>
        .stTextInput input[aria-label="Search here:"] {
            background-color: #000000;
            color: #fff600;
            font-weight: bold;
        }
    </style>
    """, unsafe_allow_html=True)
    st.header("Player search")
    name = st.text_input("Search here:")
    if name:
        found = False
        for i in range(len(players_df)):
            player = str(players_df["web_name"][i])
            first_name = str(players_df["first_name"][i])
            last_name = str(players_df["second_name"][i])
            full_name = str(players_df["first_name"][i] + " " + players_df["second_name"][i])
            ppg = float(players_df["points_per_game"][i])
            price = str(players_df["now_cost"][i] / 10)
            position_id = int(players_df["element_type"][i])
            team_id = int(players_df["team"][i])
            g_a = int(players_df["goals_scored"][i]) + int(players_df["assists"][i])
            goals = int(players_df["goals_scored"][i])
            assists = int(players_df["assists"][i])
            form = float(players_df["form"][i])
            number90s = float(round(players_df["minutes"][i] / 90, 2))
            starts = int(players_df["starts"][i])
            xG = float(players_df["expected_goals"][i])
            xA = float(players_df["expected_assists"][i])
            selected = float(players_df["selected_by_percent"][i])
            selected_rank = str(players_df["selected_rank"][i])
            ppg_rank = str(players_df["points_per_game_rank"][i])
            form_rank = str(players_df["form_rank"][i])
            price_rank = str(players_df["now_cost_rank"][i])

            # Position of Player
            if position_id == 1:
                pos = "Goalkeeper"
            elif position_id == 2:
                pos = "Defender"
            elif position_id == 3:
                pos = "Midfielder"
            elif position_id == 4:
                pos = "Forward"
            elif position_id == 5:
                pos = "Manager"

            alt_last_name = ""
            alt_name = ""
            another_alt_last_name = ""
            another_name = ""

            if " " in last_name:
                space_index = last_name.index(" ")
                alt_last_name = last_name[space_index + 1:]
                alt_name = f"{first_name} {alt_last_name}"
                another_alt_last_name = last_name[:space_index]
                another_name = f"{first_name} {another_alt_last_name}"

            possible_names = [
                player.upper(),
                first_name.upper(),
                last_name.upper(),
                full_name.upper(),
                alt_last_name.upper(),
                alt_name.upper(),
                another_name.upper(),
                another_alt_last_name.upper()
            ]

            # team_pos = str(teams_df["position"][team_id])

            team = str(teams_df["name"][team_id - 1])
           # if any(name.upper() in n for n in possible_names):
                #st.write("Player found!")
            if any(name.upper() in n for n in possible_names):
                found = True
                with (st.expander(f"{full_name} ({team} - {pos})")):
                    # st.write("Player", i)
                    # if st.button("***:rainbow[COMPARE PLAYER]***"):
                    # st.balloons()
                    st.write("**Full name:**", full_name)
                    col7, col8, col9 = st.columns(3)
                    with col7:
                        st.write("**Team:**", team)
                    with col8:
                        st.write("**Position:**", pos)
                    with col9:
                        st.write("**Price:**", "£" + price + "m")

                    st.markdown("---")
                    st.subheader("*FPL indicators:*")

                    col1, col2, col3 = st.columns(3)
                    with col1:
                        st.metric("Selected rank", selected_rank)
                        st.write("**Selected by:**", selected, "%")
                    with col2:
                        st.metric("PPG rank", ppg_rank)
                        st.write("**Points per game:**", ppg)
                    with col3:
                        st.metric("Form rank", form_rank)
                        st.write("**Form:**", form)

                    st.markdown("---")
                    st.subheader("*[LAST SEASON] Football stats:*")

                    col4, col5, col6 = st.columns(3)
                    with col4:
                        st.write("**Starts:**", starts)
                        st.write("**Full 90s completed:**", number90s)
                    with col5:
                        st.write("**Goals:**", goals)
                        st.write("**xG:**", xG)
                    with col6:
                        st.write("**Assists:**", assists)
                        st.write("**xA:**", xA)

                    st.write("**Total G/A:**", g_a)
                    st.markdown("---")
        if found:
            st.markdown(
                """
                <div style='background-color: #6dcf7b; padding: 10px; border-radius: 5px; 
                            color: white; text-align: center; font-weight: bold;'>
                 PLAYER(S) FOUND!
                </div>
                """,
                unsafe_allow_html=True)
        else:
            st.markdown(
                """
                <div style='background-color: #ff4b4b; padding: 10px; border-radius: 5px; 
                            color: white; text-align: center; font-weight: bold;'>
                    NO PLAYERS FOUND
                </div>
                """,
                unsafe_allow_html=True
            )
