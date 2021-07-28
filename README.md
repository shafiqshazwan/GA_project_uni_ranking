#Project_Uni_Ranking 
Name: Mohd Shafiq Shazwan Bin  Mohd Nizar
Course: Python Programming

The finalised coding for the project is in Project_Global_Uni_Top_1K.ipynb.

This project utilises World University Rankings datasets from Kaggle.com
The csv file chosen was the cwurData.csv.
The author of the datasets is Myles O'Neill.
source link :   https://www.kaggle.com/mylesoneill/world-university-rankings?select=cwurData.csv

Actions completed throughout the project:
1. Retrieving datasets and useful open-source libraries.
2. Cleaning the datasets.
3. Data visualisation.
4. Creating a simple application utilising the datasets.



Final
#combining uni_choice class with while loops tries

class uni_choice(object): #create a uni suggestion class
    def __init__(self, country, rank=1): #initialize 
        self.country = country
        self.rank = rank
        
    def suggest(self):
        return uni.loc[(uni['country'] == self.country) & (uni["national_rank"] == self.rank), "institution"].item() #locate the best university in any country
    
count1 = 0

while count1 !=1:  #while loop until a value exist in uni is given
    country = input("Check the best university that a country has to offer: ")
    tof1 = uni.isin([country]).any().any()  #checking if wether there are said country in the dataframe   
    
    if tof1 == True:
        count1 +=1
        
        if count1 ==1:
            unichoice=uni_choice(country) #call function in class uni_choice
            print(unichoice.suggest())
              
    else:
        print("This country doesn't hold any of the Global Top 1000 Universities. Try again with other countries...")
        count1 = 0 #keep the while loop going
        
#combining uni_ranking class with while loops tries
class uni_ranking(object): #create uni_ranking class
    def __init__(self, keyword): #initialize
        self.keyword = keyword
        
    def ranking(self):
        print(uni[["institution", str(self.keyword)]].sort_values(self.keyword))#display output as institution and selected keyword
         #sort the rankings from top to lowest

#to help keep the while loop goes if the user enter incorrect values
kywrd = ['world_rank', 'national_rank', 'quality_of_education', 'alumni_employment','quality_of_faculty','publications','influence', 'citations', 'broad_impact', 'patents']

count2 = 0
while count2 != 1:
    keyword = input("Enter any of the following")#user input the keywords for ranking
    if keyword in kywrd:
        count2 +=1
        if count2 == 1:
            uni_ranking(keyword).ranking()
            
            
    else:
        print("Put only selected values")
        count2 = 0 #reset the counter
        
#added a class to trigger the app
#final version

class gt1u_app():
    def __init__(self, start):
        self.start = start
        
    def open(self):
        
        if self.start == 'open':
            #the homepage of the app uses three inputs: ['suggest_universities, 'check_ranking, 'exit_app'
            print('Hi! Welcome to the Global Top 1000 Uni App!')
            print('Enter any of the following commands to access the app functions :   ')
            print('suggest_university= suggestion for university choice in the selected country')
            print('check_ranking = ranking of the universities in different areas')
            print('exit_app = close the app')

            count3 = 0 #this is the counter for while loop for the app homepage

            while count3 != 1:  #while loop for the app homepage  
                #user homepage input
                intro = input ('Please enter a command :   ')

                if intro == "suggest_university" :
                    count1 = 0 #loop for the uni_choice function

                    while count1 !=1:  #while loop until a value exist in uni is given
                        country = input("Check the best university that a country has to offer :   ")#uni_choice user input here
                        tof1 = uni.isin([country]).any().any()  #checking if wether there are said country in the dataframe   

                        if tof1 == True: #condition to safeguard faulty user input
                            count1 +=1

                            if count1 ==1: #function if True
                                unichoice=uni_choice(country) #call function in class uni_choice
                                print(unichoice.suggest()) #has parentheses to print the result out instead of the bound method

                        else:
                            print("This country doesn't hold any of the Global Top 1000 Universities. Try again with other countries...")
                            count1 = 0 #keep the while loop going

                    count3 = 0#need checking loop

                elif intro == "check_ranking":
                    #to help keep the while loop goes if the user enter incorrect values
                    kywrd = ['world_rank', 'national_rank', 'quality_of_education', 'alumni_employment','quality_of_faculty','publications','influence', 'citations', 'broad_impact', 'patents']

                    count2 = 0#counter for check_ranking function

                    while count2 != 1: #while loop for check_ranking
                        print('Ranking Options :   ')
                        print(kywrd) #display options to user
                        keyword = input("Enter any of the ranking preference as the following options above :   ")#uni_ranking user inputs

                        if keyword in kywrd: #checking for the keyword from the list kywrd
                            count2 +=1

                            if count2 == 1:
                                 uni_ranking(keyword).ranking()

                        else:
                            print("Put only of the given options")
                            count2 = 0 #reset the counter

                    count3=0# need checking loop

                elif intro=="exit_app":  #closing the app function
                    print('Exiting the app....')
                    print('App closed. See you later!')
                    count3 +=1

                else :
                    print("Enter only the commands provided.")#user input error safe guard
                    count3 = 0
        else:
            
            return