# Player-based-project
import sys
#def with readflie function was put
def readfile():
    #file was opened here
    f = open("players.txt")
    allplayers = []
    #range was imported 
    for i in range(20):
        player = []
        data = f.readline()
        data = data.split('; ')
        print(data)
        player_name = data[0]
        player.append(player_name)
        
        team_identifier = data[1]
        player.append(team_identifier)
        
        games_played = int(data[2])
        player.append(games_played)
        
        at_bats = int(data[3])
        player.append(at_bats)
        
        runs_scored = int(data[4])
        player.append(runs_scored)
        
        hits = int(data[5])
        player.append(hits)
        
        doubles = int(data[6])
        player.append(doubles)
        
        triples = int(data[7])
        player.append(triples)
        
        homeruns = int(data[8])
        player.append(homeruns)
        
        singles = hits - (doubles + triples + homeruns)
        total_bases = singles + 2 * doubles + 3 * triples + 4 * homeruns
        
        batting_avg = (hits) / (at_bats)
        player.append(batting_avg)
        
        slugging_percentage = (total_bases) / (at_bats)
        player.append(slugging_percentage)
        
        allplayers.append(player)
    return allplayers
#readfile was called out here
players = readfile()

def report(players_list):
    
        while True:
            
            display = input('Enter batting or slugging: ')
            display = display.lower()
            if display in ('batting', 'slugging'):
                if display == 'batting':
                    f = open('players_battingaverage.txt', 'w')
                    for i in players_list:  
                        f.write(str(i))   
                elif display == 'slugging':
                    f = open('players_sluggingpercentage.txt', 'w')
                    for i in players_list:  
                        f.write(str(i))   
                break
            else:
                print('Please enter a valid report name')
                


def inputcommand(myplayers):
    
                          
    command = input('Type your command: ')
    command = command.lower()
    if command == 'quit':
        sys.exit()
    elif command == 'help':
        print('These are the commands you should enter')
        print('QUIT: If you want to quit')
        print('HELP: for getting help about the commands')
        print('TEAM: for getting details about the team')
        print('REPORT: to report the batting or slugging')
        
    elif command == 'team':
        team_id = input('Enter the team identifier: ')
        for i in myplayers:
            if team_id == i[1]:
                for x in i:
                    print(x, end = ' ')
            elif team_id not in ('CWS', 'DET', 'LAA', 'CIN', 'ATL', 'SF',
                                 'NYY', 'STL', 'SD', 'CLE', 'TEX', 'HOU', 'COL',
                                 'CHC', 'NYM'):
                print('You entered an invalid team name')

    elif command == 'report':
        report(myplayers)
        
inputcommand(players)

