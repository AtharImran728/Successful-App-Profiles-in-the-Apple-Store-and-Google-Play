# Successful App Profiles in the Apple Store and Google Play

Our aim in this project is to find mobile app profiles that are profitable for the App Store and Google Play markets. We're working as data analysts for a company that builds Android and iOS mobile apps, and our job is to enable our team of developers to make data-driven decisions with respect to the kind of apps they build.

At our company, we only build apps that are free to download and install, and our main source of revenue consists of in-app ads. This means that our revenue for any given app is mostly influenced by the number of users that use our app. Our goal for this project is to analyze data to help our developers understand what kinds of apps are likely to attract more users.


#### -- Project Status: [Completed]
#### -- Langauges: [Python]

### Sources:
There are over 4 million apps available on the App Store and Google Play. Collecting data for all of these apps would be too time-consuming and expensive. Instead, we will analyze a sample of data.

 Two data sets that seem suitable for our purpose contain data about 10,000 Android apps from [Google Playstore app](https://www.kaggle.com/lava18/google-play-store-apps) and 7,000 iOS apps from the [Apple Store](https://www.kaggle.com/datasets/ramamet4/app-store-apple-data-set-10k-apps).

elow is first few rows of Google Playstore Data set:

 App|Category|Rating|Reviews|Size|Installs|Type|Price|Content Rating|
| - | - | - | - | - | - | - | - | - |
|Photo Editor & Candy Camera & Grid & ScrapBook|ART\_AND\_DESIGN|4\.1|159|19M|10,000+|Free|0|Everyone|
|Coloring book moana|ART\_AND\_DESIGN|3\.9|967|14M|500,000+|Free|0|Everyone|
|U Launcher Lite – FREE Live Cool Themes, Hide Apps|ART\_AND\_DESIGN|4\.7|87510|8\.7M|5,000,000+|Free|0|Everyone|
|Sketch - Draw & Paint|ART\_AND\_DESIGN|4\.5|215644|25M|50,000,000+|Free|0|Teen||

And first few rows of  Apple store Data set:

||id|track\_name|size\_bytes|currency|price|rating\_count\_tot|rating\_count\_ver|user\_rating|
| - | - | - | - | - | - | - | - | - |
|1|2\.82E+08|PAC-MAN Premium|1\.01E+08|USD|3\.99|21292|26|4|
|2|2\.82E+08|Evernote - stay organized|1\.59E+08|USD|0|161065|26|4|
|3|2\.82E+08|WeatherBug - Local Weather, Radar, Maps, Alerts|1\.01E+08|USD|0|188583|2822|3\.5|
|4|2\.83E+08|eBay: Best App to Buy, Sell, Save! Online Shopping|1\.29E+08|USD|0|262241|649|4|

## Objectives :
To reach our goals, we'll:

- **Identify the most profitable app profiles.**
We will analyze data from the App Store and Google Play to identify the app profiles that are most likely to be profitable.

- **Examine the factors that contribute to profitability.**
We will explore the factors that contribute to profitability, such as app category, user engagement, and monetization strategy.

- **Identify opportunities for improvement.**
We will use our findings to identify opportunities for improvement in our own app development process.

These are the main objectives for the project. We will also need to perform other tasks, such as cleaning the data and visualizing the results. However, these three objectives are the most important.

## Blockers and Challenges

 The main blockers and challenges that I am facing with this project include:
 
- **Data quality:** The data that we are using may not be perfect. There may be duplicate rows, errors, non english apps or missing values. This could make it difficult to analyze the data and identify trends.

- **App store policies:** The app stores have different policies that developers need to follow. For example, the App Store has a policy that apps cannot be clones of other apps. This could limit the number of apps that we can analyze.

- **Market competition:** The app markets are very competitive. There are millions of apps available, and it can be difficult to stand out from the crowd. This could make it difficult to make a profit from our app.

These are just some of the blockers and challenges that the project might face. It is important to be aware of these challenges so that we can plan accordingly.

## Needs of this project

- **To help the company make data-driven decisions about which apps to build.** The company wants to build apps that are likely to be profitable, so they need to understand what kind of apps are popular and successful. This project will help them to identify the most popular genres of apps, as well as the features that are most important to users.

- **To improve the company's app store optimization (ASO) strategy.** [ASO](https://www.storemaven.com/academy/winning-aso-strategy-components/#:~:text=An%20ASO%20strategy%20is%20a,app%20marketing%20and%20growth%20strategy.) is the process of optimizing an app's listing in the app store so that it is more likely to be found by users. This project will help the company to understand what factors are important for ASO, such as the app's title, description, and keywords.

- **To provide insights into the mobile app market.** The company wants to understand the mobile app market so that they can make informed decisions about their app development strategy. This project will provide them with data on the most popular genres of apps, the features that are most important to users, and the trends in the mobile app market.

Overall, this project will help the company to make data-driven decisions about which apps to build, improve their ASO strategy, and understand the mobile app market. This will allow them to build more successful apps and grow their busines

## Opening and Exploring the Data
Let's start by opening the two data sets and then continue with exploring the data.
``` python
from csv import reader

### The Google Play data set ###
opened_file = open('googleplaystore.csv')
read_file = reader(opened_file)
android = list(read_file)
android_header = android[0]
android = android[1:]

### The App Store data set ###
opened_file = open('AppleStore.csv')
read_file = reader(opened_file)
ios = list(read_file)
ios_header = ios[0]
ios = ios[1:]
```

To make it easier to explore the two data sets, we'll first write a function named `explore_data()` that we can use repeatedly to explore rows in a more readable way. We'll also add an option for our function to show the number of rows and columns for any data set.

*Code:*
```python
def explore_data(dataset, start, end, rows_and_columns=False):
    dataset_slice = dataset[start:end]    
    for row in dataset_slice:
        print(row)
        print('\n') # adds a new (empty) line between rows
        
    if rows_and_columns:
        print('Number of rows:', len(dataset))
        print('Number of columns:', len(dataset[0]))

print(android_header)
print('\n')
explore_data(android, 0, 3, True)
```
*Output:*
```
['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver']


['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']


['Coloring book moana', 'ART_AND_DESIGN', '3.9', '967', '14M', '500,000+', 'Free', '0', 'Everyone', 'Art & Design;Pretend Play', 'January 15, 2018', '2.0.0', '4.0.3 and up']


['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']


Number of rows: 10841
Number of columns: 13
```

We see that the Google Play data set has *10841 apps and 13 columns*. At a quick glance, the columns that might be useful for the purpose of our analysis are `'App'`, `'Category'`, `'Reviews'`, `'Installs'`, `'Type'`, `'Price'`, and `'Genres'`.

Now let's take a look at the App Store data set.

*Code:*
```python
print(ios_header)
print('\n')
explore_data(ios, 0, 3, True)
```

*Output*
```
['id', 'track_name', 'size_bytes', 'currency', 'price', 'rating_count_tot', 'rating_count_ver', 'user_rating', 'user_rating_ver', 'ver', 'cont_rating', 'prime_genre', 'sup_devices.num', 'ipadSc_urls.num', 'lang.num', 'vpp_lic']


['284882215', 'Facebook', '389879808', 'USD', '0.0', '2974676', '212', '3.5', '3.5', '95.0', '4+', 'Social Networking', '37', '1', '29', '1']


['389801252', 'Instagram', '113954816', 'USD', '0.0', '2161558', '1289', '4.5', '4.0', '10.23', '12+', 'Photo & Video', '37', '0', '29', '1']


['529479190', 'Clash of Clans', '116476928', 'USD', '0.0', '2130805', '579', '4.5', '4.5', '9.24.12', '9+', 'Games', '38', '5', '18', '1']


Number of rows: 7197
Number of columns: 16
```
We have *7197 iOS apps* in this data set, and the columns that seem interesting are: `'track_name'`, `'currency'`, `'price'`, `'rating_count_tot'`, `'rating_count_ver'`, and `'prime_genre'`.



## Data cleaning
The following steps will be taken to clean the data:

1- **Removing Duplicate Entries:**  The dataset contains many duplicate apps, which can skew our analysis. We will remove these duplicates to ensure that our results are accurate.

2- **Removing Non-English Apps:** Our company only builds English-language apps, so we will remove all non-English apps from the dataset. This will allow us to focus our analysis on the apps that are relevant to our business.

3- **Isolating the Free Apps:** Our company only builds free apps, so we will isolate the free apps from the dataset. This will allow us to focus our analysis on the apps that are most relevant to our business model.

### 1- Removing Duplicate Entries:

If we explore the Google Play data set long enough, we'll find that some apps have more than one entry. For instance, the application Instagram has four entries:

*Code*
```python
for app in android:
    name = app[0]
    if name == 'Instagram':
        print(app)
```
*Output:*
```
['Instagram', 'SOCIAL', '4.5', '66577313', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
['Instagram', 'SOCIAL', '4.5', '66577446', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
['Instagram', 'SOCIAL', '4.5', '66577313', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
['Instagram', 'SOCIAL', '4.5', '66509917', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
```

In total, there are 1,181 cases where an app occurs more than once:

*Code:*
```python
duplicate_apps = []
unique_apps = []

for app in android:
    name = app[0]
    if name in unique_apps:
        duplicate_apps.append(name)
    else:
        unique_apps.append(name)
    
print('Number of duplicate apps:', len(duplicate_apps))
print('\n')
print('Examples of duplicate apps:', duplicate_apps[:15])
```

*Output:*
```
Number of duplicate apps: 1181

Examples of duplicate apps: ['Quick PDF Scanner + OCR FREE', 'Box', 'Google My Business', 'ZOOM Cloud Meetings', 'join.me - Simple Meetings', 'Box', 'Zenefits', 'Google Ads', 'Google My Business', 'Slack', 'FreshBooks Classic', 'Insightly CRM', 'QuickBooks Accounting: Invoicing & Expenses', 'HipChat - Chat Built for Teams', 'Xero Accounting Software']
```

We don't want to count certain apps more than once when we analyze data, so we need to remove the duplicate entries and keep only one entry per app. One thing we could do is remove the duplicate rows randomly, but we could probably find a better way.

Here duplicate apps exist because the data is collected at different time. So, the latest time should have the latest rating. We won't remove rows randomly, but rather we'll keep the rows that have the highest number of reviews because the higher the number of reviews, the more reliable the ratings.

To do that, we will:

- Create a dictionary where each key is a unique app name, and the value is the highest number of reviews of that app
- Use the dictionary to create a new data set, which will have only one entry per app (and we only select the apps with the highest number of reviews)

#### Building the dictionary
Let's start by building the dictionary.

*Code:*
```python
reviews_max = {}

for app in android:
    name = app[0]
    n_reviews = float(app[3])
    
    if name in reviews_max and reviews_max[name] < n_reviews:
        reviews_max[name] = n_reviews
        
    elif name not in reviews_max:
        reviews_max[name] = n_reviews
```

In a previous code cell, we found that there are *1,181 cases* where an app occurs more than once, so the length of our dictionary (of unique apps) should be equal to the difference between the length of our data set and 1,181.

*Code:*
```python
print('Expected length:', len(android) - 1181)
print('Actual length:', len(reviews_max))
```
*Output:*
```
Expected length: 9659
Actual length: 9659
```

Now, let's use the `reviews_max` dictionary to remove the duplicates. For the duplicate cases, we'll only keep the entries with the highest number of reviews. In the code cell below:

- We start by initializing two empty lists, `android_clean` and `already_added`.
- We loop through the Android data set, and for every iteration:

   - We isolate the name of the app and the number of reviews.

   - We add the current row (app) to the `android_clean` list, and the app name (name) to the `already_added` list if:

       - The number of reviews of the current app matches the number of reviews of that app as described in the `reviews_max dictionary`; and

        - The name of the app is not already in the `already_added` list. We need to add this supplementary condition to account for those cases where the highest number of reviews of a duplicate app is the same for more than one entry (for example, the Box app has three entries, and the number of reviews is the same). If we just check for `reviews_max[name] == n_reviews`, we'll still end up with duplicate entries for some apps.

*Code:*
```python       
android_clean = []
already_added = []

for app in android:
    name = app[0]
    n_reviews = float(app[3])
    
    if (reviews_max[name] == n_reviews) and (name not in already_added):
        android_clean.append(app)
        already_added.append(name) # make sure this is inside the if block
```

Now let's quickly explore the new data set, and confirm that the number of rows is 9,659.

*Code:*
```python
explore_data(android_clean, 0, 3, True)
```
*Output:*
```
['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']


['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']


['Sketch - Draw & Paint', 'ART_AND_DESIGN', '4.5', '215644', '25M', '50,000,000+', 'Free', '0', 'Teen', 'Art & Design', 'June 8, 2018', 'Varies with device', '4.2 and up']

Number of rows: 9659
Number of columns: 13
``` 

We have 9659 rows, just as expected.


### Removing Non-English Apps

If you explore the data sets enough, you'll notice the names of some of the apps suggest they are not directed toward an English-speaking audience. Below, we see a couple of examples from both data sets:

*Code:*
```python
print(ios[813][1])
print(ios[6731][1])

print(android_clean[4412][0])
print(android_clean[7940][0])
```
*Output:*
```
爱奇艺PPS -《欢乐颂2》电视剧热播
【脱出ゲーム】絶対に最後までプレイしないで 〜謎解き＆ブロックパズル〜
中国語 AQリスニング
لعبة تقدر تربح DZ
```

We're not interested in keeping these kind of apps, so we'll remove them. One way to go about this is to remove each app whose name contains a symbol that is not commonly used in English text — English text usually includes letters from the English alphabet, numbers composed of digits from 0 to 9, punctuation marks (., !, ?, ;, etc.), and other symbols (+, *, /, etc.).

All these characters that are specific to English texts are encoded using the `ASCII standard`. Each ASCII character has a corresponding number between 0 and 127 associated with it, and we can take advantage of that to build a function that checks an app name and tells us whether it contains non-ASCII characters.

We built this function below, and we use the built-in `ord()` function to find out the corresponding encoding number of each character.

*Code:*
```python
def is_english(string):
    
    for character in string:
        if ord(character) > 127:
            return False
    
    return True

print(is_english('Instagram'))
print(is_english('爱奇艺PPS -《欢乐颂2》电视剧热播'))
True
False
The function seems to work fine, but some English app names use emojis or other symbols (™, — (em dash), – (en dash), etc.) that fall outside of the ASCII range. Because of this, we'll remove useful apps if we use the function in its current form.

print(is_english('Docs To Go™ Free Office Suite'))
print(is_english('Instachat 😜'))

print(ord('™'))
print(ord('😜'))
```
*Output:*
```
False
False
8482
128540
```


To minimize the impact of data loss, we'll only remove an app if its name has more than three non-ASCII characters:

*Code:*
```python
def is_english(string):
    non_ascii = 0
    
    for character in string:
        if ord(character) > 127:
            non_ascii += 1
    
    if non_ascii > 3:
        return False
    else:
        return True

print(is_english('Docs To Go™ Free Office Suite'))
print(is_english('Instachat 😜'))
```
*Output:*
```
True
True
```

The function is still not perfect, and very few non-English apps might get past our filter, but this seems good enough at this point in our analysis — we shouldn't spend too much time on optimization at this point.

Below, we use the `is_english()` function to filter out the non-English apps for both data sets:

*Code:*
```python
android_english = []
ios_english = []

for app in android_clean:
    name = app[0]
    if is_english(name):
        android_english.append(app)
        
for app in ios:
    name = app[1]
    if is_english(name):
        ios_english.append(app)
        
explore_data(android_english, 0, 3, True)
print('\n')
explore_data(ios_english, 0, 3, True)
```
*Output:*
```
['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']


['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']


['Sketch - Draw & Paint', 'ART_AND_DESIGN', '4.5', '215644', '25M', '50,000,000+', 'Free', '0', 'Teen', 'Art & Design', 'June 8, 2018', 'Varies with device', '4.2 and up']


Number of rows: 9614
Number of columns: 13


['284882215', 'Facebook', '389879808', 'USD', '0.0', '2974676', '212', '3.5', '3.5', '95.0', '4+', 'Social Networking', '37', '1', '29', '1']


['389801252', 'Instagram', '113954816', 'USD', '0.0', '2161558', '1289', '4.5', '4.0', '10.23', '12+', 'Photo & Video', '37', '0', '29', '1']


['529479190', 'Clash of Clans', '116476928', 'USD', '0.0', '2130805', '579', '4.5', '4.5', '9.24.12', '9+', 'Games', '38', '5', '18', '1']


Number of rows: 6183
Number of columns: 16
```

We can see that we're left with 9614 Android apps and 6183 iOS apps.

### Isolating the Free Apps

As we mentioned, we only build apps that are free to download and install, and our main source of revenue consists of in-app ads. Our data sets contain both free and non-free apps, and we'll need to isolate only the free apps for our analysis. Below, we isolate the free apps for both our data sets.

*Code:*
```python
android_final = []
ios_final = []

for app in android_english:
    price = app[7]
    if price == '0':
        android_final.append(app)
        
for app in ios_english:
    price = app[4]
    if price == '0.0':
        ios_final.append(app)
        
print(len(android_final))
print(len(ios_final))
```
*Output:*
```
8864
3222
```
We're left with,
-  8864 Android apps,
- 3222 iOS apps

 which should be enough for our analysis.

## Most Common Apps by Genre

As we mentioned in the introduction, our aim is to determine the kinds of apps that are likely to attract more users because our revenue is highly influenced by the number of people using our apps.

To minimize risks and overhead, our validation strategy for an app idea is comprised of three steps:

- Build a minimal Android version of the app, and add it to Google Play.

- If the app has a good response from users, we then develop it further.
- If the app is profitable after six months, we also build an iOS version of the app and add it to the App Store.
- Because our end goal is to add the app on both the App Store and Google Play, we need to find app profiles that are successful on both markets. For instance, a profile that might work well for both markets might be a productivity app that makes use of gamification.

Let's begin the analysis by getting a sense of the most common genres for each market. For this, we'll build a frequency table for the `prime_genre column` of the App Store data set, and the Genres and Category columns of the Google Play data set.


We'll build two functions we can use to analyze the frequency tables:

- One function to generate frequency tables that show percentages
- Another function that we can use to display the percentages in a descending order

*Code:*
```python
def freq_table(dataset, index):
    table = {}
    total = 0
    
    for row in dataset:
        total += 1
        value = row[index]
        if value in table:
            table[value] += 1
        else:
            table[value] = 1
    
    table_percentages = {}
    for key in table:
        percentage = (table[key] / total) * 100
        table_percentages[key] = percentage 
    
    return table_percentages


def display_table(dataset, index):
    table = freq_table(dataset, index)
    table_display = []
    for key in table:
        key_val_as_tuple = (table[key], key)
        table_display.append(key_val_as_tuple)
        
    table_sorted = sorted(table_display, reverse = True)
    for entry in table_sorted:
        print(entry[1], ':', entry[0])
```

We start by examining the frequency table for the `prime_genre` column of the App Store data set.

*Code:*
```python
display_table(ios_final, -5)
```
*Output (as table):*
|Catagory|Percentage|
|---|---|
Games | 58.162
Entertainment | 3.63
Social Networking | 3.28
Shopping | 2.607
Utilities | 2.513
Sports| 2.141
Music | 2.0484
Health & Fitness | 2.01
Productivity | 1.738
Lifestyle | 1.58286
News | 1.3345
Travel | 1.2414
Finance | 1.117318
Weather | 0.869
Food & Drink | 0.806
Reference | 0.558
Business | 0.527
Book | 0.434
Navigation | 0.186
Medical | 0.186
Catalogs | 0.1241


We can see that among the free English apps, more than a half (58.16%) are games. Entertainment apps are close to 8%, followed by photo and video apps, which are close to 5%. Only 3.66% of the apps are designed for education, followed by social networking apps which amount for 3.29% of the apps in our data set.

#### Free English Apps by Category

| Category | Percentage |
|---|---|
| Games | 58.16% |
| Entertainment | 7.98% |
| Photo & Video | 4.99% |
| Productivity | 4.33% |
| Social Networking | 3.29% |
| Education | 3.66% |
| Other | 18.49% |

Total: 100%

The general impression is that App Store (at least the part containing free English apps) is dominated by apps that are designed for fun (games, entertainment, photo and video, social networking, sports, music, etc.), while apps with practical purposes (education, shopping, utilities, productivity, lifestyle, etc.) are more rare. However, the fact that fun apps are the most numerous doesn't also imply that they also have the greatest number of users — the demand might not be the same as the offer.

Let's continue by examining the Genres and Category columns of the Google Play data set (two columns which seem to be related).

*Code:*
```python
display_table(android_final, 1) # Category
```

*Output (as table):*
| Category | Percentage |
|---|---|
| Family | 18.90% |
| Games | 9.72% |
| Tools | 8.46% |
| Business | 4.59% |
| Lifestyle | 3.90% |
| Productivity | 3.89% |
| Finance | 3.70% |
| Medical | 3.53% |
| Sports | 3.39% |
| **Personalization** | 3.31% |
| **Communication** | 3.23% |
| **Health & Fitness** | 3.08% |
| **Photography** | 2.94% |
| **News & Magazines** | 2.79% |
| **Social** | 2.66% |
| **Travel & Local** | 2.33% |
| **Shopping** | 2.24% |
| **Books & Reference** | 2.14% |
| **Dating** | 1.86% |
| **Video Players** | 1.79% |
| **Maps & Navigation** | 1.39% |
| **Food & Drink** | 1.24% |
| **Education** | 1.16% |
| **Entertainment** | 0.96% |
| **Libraries & Demo** | 0.94% |
| **Auto & Vehicles** | 0.92% |
| **House & Home** | 0.82% |
| **Weather** | 0.80% |
| **Events** | 0.71% |
| **Parenting** | 0.65% |
| **Art & Design** | 0.64% |
| **Comics** | 0.62% |
| **Beauty** | 0.59% |

Total: 100%

The landscape seems significantly different on Google Play: there are not that many apps designed for fun, and it seems that a good number of apps are designed for practical purposes (family, tools, business, lifestyle, productivity, etc.). However, if we investigate this further, we can see that the family category (which accounts for almost 19% of the apps) means mostly games for kids.

![App Screenshot](https://camo.githubusercontent.com/0d974d86dfcb791ca1d1505f810ba5a191bb6248e413d9b6ae1a60b211cca918/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f64712d636f6e74656e742f3335302f7079316d385f66616d696c792e706e67)

Even so, practical apps seem to have a better representation on Google Play compared to App Store. This picture is also confirmed by the frequency table we see for the Genres column:

*Code:*
```python
display_table(android_final, -4)
```
*Output (as table):*
| Category | Genre | Percentage |
|---|---|---|
| Tools | Productivity | 12.40% |
| Tools | Communication | 10.15% |
| Tools | Utility | 8.20% |
| Entertainment | Games | 16.92% |
| Entertainment | Music & Video | 12.81% |
| Entertainment | Books & Reference | 6.77% |
| Education | Educational | 13.54% |
| Education | Brain Games | 6.77% |
| Education | Pretend Play | 6.77% |
| Family | Pretend Play | 6.77% |
| Casual | Brain Games | 4.51% |
| Casual | Action & Adventure | 4.51% |
| Arcade | Action & Adventure | 3.38% |
| Action | Action & Adventure | 2.25% |
| Racing | Action & Adventure | 2.25% |
| Simulation | Action & Adventure | 2.25% |
| Sports | Action & Adventure | 2.25% |
| Strategy | Action & Adventure | 2.25% |
| Adventure | Action & Adventure | 2.25% |
| Puzzle | Brain Games | 2.25% |
| Trivia | Education | 2.25% |
| Travel & Local | Action & Adventure | 2.25% |

Total: 100%

The difference between the Genres and the Category columns is not crystal clear, but one thing we can notice is that the Genres column is much more granular (it has more categories). We're only looking for the bigger picture at the moment, so we'll only work with the Category column moving forward.

Up to this point, we found that the App Store is dominated by apps designed for fun, while Google Play shows a more balanced landscape of both practical and for-fun apps. Now we'd like to get an idea about the kind of apps that have most users.

Most Popular Apps by Genre on the App Store
One way to find out what genres are the most popular (have the most users) is to calculate the average number of installs for each app genre. For the Google Play data set, we can find this information in the Installs column, but for the App Store data set this information is missing. As a workaround, we'll take the total number of user ratings as a proxy, which we can find in the rating_count_tot app.

Below, we calculate the average number of user ratings per app genre on the App Store:

*Code:*
```python
genres_ios = freq_table(ios_final, -5)

for genre in genres_ios:
    total = 0
    len_genre = 0
    for app in ios_final:
        genre_app = app[-5]
        if genre_app == genre:            
            n_ratings = float(app[5])
            total += n_ratings
            len_genre += 1
    avg_n_ratings = total / len_genre
    print(genre, ':', avg_n_ratings)
```
*Output (as table):*
| Category | Installs |
|---|---|
| Social Networking | 71,548.34905660378 |
| Photo & Video | 28,441.54375 |
| Games | 22,788.6696905016 |
| Music | 57,326.530303030304 |
| Reference | 74,942.11111111111 |
| Health & Fitness | 23,298.015384615384 |
| Weather | 52,279.892857142855 |
| Utilities | 18,684.456790123455 |
| Travel | 28,243.8 |
| Shopping | 26,919.690476190477 |
| News | 21,248.023255813954 |
| Navigation | 86,090.33333333333 |
| Lifestyle | 16,485.764705882353 |
| Entertainment | 14,029.830708661417 |
| Food & Drink | 33,333.92307692308 |
| Sports | 23,008.898550724636 |
| Book | 39,758.5 |
| Finance | 31,467.944444444445 |
| Education | 7,003.983050847458 |
| Productivity | 21,028.410714285714 |
| Business | 7,491.117647058823 |
| Catalogs | 4,004.0 |
| Medical | 612.0 |

Total installs: 2,028,152

On average, navigation apps have the highest number of user reviews, but this figure is heavily influenced by Waze and Google Maps, which have close to half a million user reviews together:

*Code:*
```python
for app in ios_final:
    if app[-5] == 'Navigation':
        print(app[1], ':', app[5]) # print name and number of ratings
```
*Output (as table):*
| App | Installs |
|---|---|
| Waze - GPS Navigation, Maps & Real-time Traffic | 345,046 |
| Google Maps - Navigation & Transit | 154,911 |
| Geocaching® | 12,811 |
| CoPilot GPS – Car Navigation & Offline Maps | 3,582 |
| ImmobilienScout24: Real Estate Search in Germany | 187 |
| Railway Route Search | 5 |
|**Total installs:**| 516,641|

The same pattern applies to social networking apps, where the average number is heavily influenced by a few giants like Facebook, Pinterest, Skype, etc. Same applies to music apps, where a few big players like Pandora, Spotify, and Shazam heavily influence the average number.

Our aim is to find popular genres, but navigation, social networking or music apps might seem more popular than they really are. The average number of ratings seem to be skewed by very few apps which have hundreds of thousands of user ratings, while the other apps may struggle to get past the 10,000 threshold. We could get a better picture by removing these extremely popular apps for each genre and then rework the averages, but we'll leave this level of detail for later.

Reference apps have 74,942 user ratings on average, but it's actually the Bible and Dictionary.com which skew up the average rating:

*Code:*
```python
for app in ios_final:
    if app[-5] == 'Reference':
        print(app[1], ':', app[5])
```
*Output (as table):*
|Name|Rating|
|--|--|
Bible | 985920
Dictionary.com Dictionary & Thesaurus | 200047
Dictionary.com Dictionary & Thesaurus for iPad | 54175
Google Translate | 26786
Muslim Pro: Ramadan 2017 Prayer Times, Azan, Quran | 18418
New Furniture Mods - Pocket Wiki & Game Tools for Minecraft PC Edition | 17588
Merriam-Webster Dictionary | 16849
Night Sky | 12122
City Maps for Minecraft PE - The Best Maps for Minecraft Pocket Edition (MCPE) | 8535
LUCKY BLOCK MOD ™ for Minecraft PC Edition - The Best Pocket Wiki & Mods Installer Tools | 4693
GUNS MODS for Minecraft PC Edition - Mods Tools | 1497
Guides for Pokémon GO - Pokemon GO News and Cheats | 826
WWDC | 762
Horror Maps for Minecraft PE - Download The Scariest Maps for Minecraft Pocket Edition (MCPE) Free | 718
VPN Express | 14
Real Bike Traffic Rider Virtual Reality Glasses : 8
教えて!goo | 0
Jishokun-Japanese English Dictionary & Translator | 0

However, this niche seems to show some potential. One thing we could do is take another popular book and turn it into an app where we could add different features besides the raw version of the book. This might include daily quotes from the book, an audio version of the book, quizzes about the book, etc. On top of that, we could also embed a dictionary within the app, so users don't need to exit our app to look up words in an external app.

This idea seems to fit well with the fact that the App Store is dominated by for-fun apps. This suggests the market might be a bit saturated with for-fun apps, which means a practical app might have more of a chance to stand out among the huge number of apps on the App Store.

Other genres that seem popular include weather, book, food and drink, or finance. The book genre seem to overlap a bit with the app idea we described above, but the other genres don't seem too interesting to us:

> Weather apps — people generally don't spend too much time in-app, and the chances of making profit from in-app adds are low. Also, getting reliable live weather data may require us to connect our apps to non-free APIs.

> Food and drink — examples here include Starbucks, Dunkin' Donuts, McDonald's, etc. So making a popular food and drink app requires actual cooking and a delivery service, which is outside the scope of our company.

> Finance apps — these apps involve banking, paying bills, money transfer, etc. Building a finance app requires domain knowledge, and we don't want to hire a finance expert just to build an app.

Now let's analyze the Google Play market a bit.

Most Popular Apps by Genre on Google Play
For the Google Play market, we actually have data about the number of installs, so we should be able to get a clearer picture about genre popularity. However, the install numbers don't seem precise enough — we can see that most values are open-ended (100+, 1,000+, 5,000+, etc.):

*Code:*
```python
display_table(android_final, 5) # the Installs columns
```
*Output:*
|Downloads|Percentage|
|--|--|
1,000,000+ | 15.72
100,000+ | 11.552
10,000,000+ | 10.548
10,000+ | 10.198
1,000+ | 8.39
100+ | 6.915
5,000,000+ | 6.82
500,000+ | 5.561
50,000+ | 4.7
5,000+ | 4.512
10+ | 3.5424
500+ | 3.2490
50,000,000+ | 2.301
100,000,000+ | 2.132
50+ | 1.917
5+ | 0.789
1+ | 0.5076
500,000,000+ | 0.2707
1,000,000,000+ | 0.22
0+ | 0.0451
0 | 0.011

One problem with this data is that is not precise. For instance, we don't know whether an app with 100,000+ installs has 100,000 installs, 200,000, or 350,000. However, we don't need very precise data for our purposes — we only want to get an idea which app genres attract the most users, and we don't need perfect precision with respect to the number of users.

We're going to leave the numbers as they are, which means that we'll consider that an app with 100,000+ installs has 100,000 installs, and an app with 1,000,000+ installs has 1,000,000 installs, and so on.

To perform computations, however, we'll need to convert each install number to float — this means that we need to remove the commas and the plus characters, otherwise the conversion will fail and raise an error. We'll do this directly in the loop below, where we also compute the average number of installs for each genre (category).

*Code:*
```python
categories_android = freq_table(android_final, 1)

for category in categories_android:
    total = 0
    len_category = 0
    for app in android_final:
        category_app = app[1]
        if category_app == category:            
            n_installs = app[5]
            n_installs = n_installs.replace(',', '')
            n_installs = n_installs.replace('+', '')
            total += float(n_installs)
            len_category += 1
    avg_n_installs = total / len_category
    print(category, ':', avg_n_installs)
```
*Output (as table):*
| Category | Installs |
|---|---|
| ART_AND_DESIGN | 19,863,350.877192982 |
| AUTO_AND_VEHICLES | 6,473,178.170731707 |
| BEAUTY | 5,131,518.867924528 |
| BOOKS_AND_REFERENCE | 8,767,811.894736841 |
| BUSINESS | 17,122,901.47420147 |
| COMICS | 8,176,572.727272727 |
| COMMUNICATION | 38,456,119.167247385 |
| DATING | 8,540,288.83030303 |
| EDUCATION | 18,334,951.45631068 |
| ENTERTAINMENT | 11,640,705.88235294 |
| EVENTS | 2,535,422.2222222222 |
| FINANCE | 13,876,924.75609756 |
| FOOD_AND_DRINK | 1,924,897.7363636363 |
| HEALTH_AND_FITNESS | 41,888,219.853479853 |
| HOUSE_AND_HOME | 1,331,540.5616438356 |
| LIBRARIES_AND_DEMO | 6,385,037.34939759 |
| LIFESTYLE | 1,437,816.2687861272 |
| GAME | 15,588,015.603248259 |
| FAMILY | 3,695,641.8198090694 |
| MEDICAL | 120,550.61980830671 |
| SOCIAL | 23,253,652.127118643 |
| SHOPPING | 7,036,877.311557789 |
| PHOTOGRAPHY | 17,840,110.40229885 |
| SPORTS | 3,638,640.1428571427 |
| TRAVEL_AND_LOCAL | 13,984,077.710144928 |
| TOOLS | 10,801,391.298666667 |
| PERSONALIZATION | 5,201,482.6122448975 |
| PRODUCTIVITY | 16,787,331.344927534 |
| PARENTING | 542,603.6206896552 |
| WEATHER | 5,074,486.197183099 |
| VIDEO_PLAYERS | 24,727,872.452830188 |
| NEWS_AND_MAGAZINES | 9,549,178.467741935 |
| MAPS_AND_NAVIGATION | 4,056,941.7741935486 |

On average, communication apps have the most installs: 38,456,119. This number is heavily skewed up by a few apps that have over one billion installs (WhatsApp, Facebook Messenger, Skype, Google Chrome, Gmail, and Hangouts), and a few others with over 100 and 500 million installs:

*Code:*
```python
for app in android_final:
    if app[1] == 'COMMUNICATION' and (app[5] == '1,000,000,000+'
                                      or app[5] == '500,000,000+'
                                      or app[5] == '100,000,000+'):
        print(app[0], ':', app[5])
```
*Output (as table):*

| App Name                                         | Number of Downloads                |
|:--------------------------------------------------|-----------------------------------|
| WhatsApp Messenger                               | 1,000,000,000+                   |
| imo beta free calls and text                     | 100,000,000+                     |
| Android Messages                                | 100,000,000+                     |
| Google Duo - High Quality Video Calls            | 500,000,000+                     |
| Messenger – Text and Video Chat for Free         | 1,000,000,000+                   |
| imo free video calls and chat                    | 500,000,000+                     |
| Skype - free IM & video calls                    | 1,000,000,000+                   |
| Who                                              | 100,000,000+                     |
| GO SMS Pro - Messenger, Free Themes, Emoji       | 100,000,000+                     |
| LINE: Free Calls & Messages                      | 500,000,000+                     |
| Google Chrome: Fast & Secure                     | 1,000,000,000+                   |
| Firefox Browser fast & private                   | 100,000,000+                     |
| UC Browser - Fast Download Private & Secure      | 500,000,000+                     |
| Gmail                                            | 1,000,000,000+                   |
| Hangouts                                        | 1,000,000,000+                   |
| Messenger Lite: Free Calls & Messages            | 100,000,000+                     |
| Kik                                              | 100,000,000+                     |
| KakaoTalk: Free Calls & Text                     | 100,000,000+                     |
| Opera Mini - fast web browser                    | 100,000,000+                     |
| Opera Browser: Fast and Secure                   | 100,000,000+                     |
| Telegram                                        | 100,000,000+                     |
| Truecaller: Caller ID, SMS spam blocking & Dialer | 100,000,000+                     |
| UC Browser Mini -Tiny Fast Private & Secure      | 100,000,000+                     |
| Viber Messenger                                 | 500,000,000+                     |
| WeChat                                           | 100,000,000+                     |
| Yahoo Mail – Stay Organized                      | 100,000,000+                     |
| BBM - Free Calls & Messages                      | 100,000,000+                     |


If we removed all the communication apps that have over 100 million installs, the average would be reduced roughly ten times:

*Code:*
```python
under_100_m = []

for app in android_final:
    n_installs = app[5]
    n_installs = n_installs.replace(',', '')
    n_installs = n_installs.replace('+', '')
    if (app[1] == 'COMMUNICATION') and (float(n_installs) < 100000000):
        under_100_m.append(float(n_installs))
        
sum(under_100_m) / len(under_100_m)
```
*Output:*
```
3603485.3884615386
```
We see the same pattern for the video players category, which is the runner-up with 24,727,872 installs. The market is dominated by apps like Youtube, Google Play Movies & TV, or MX Player. The pattern is repeated for social apps (where we have giants like Facebook, Instagram, Google+, etc.), photography apps (Google Photos and other popular photo editors), or productivity apps (Microsoft Word, Dropbox, Google Calendar, Evernote, etc.).

Again, the main concern is that these app genres might seem more popular than they really are. Moreover, these niches seem to be dominated by a few giants who are hard to compete against.

The game genre seems pretty popular, but previously we found out this part of the market seems a bit saturated, so we'd like to come up with a different app recommendation if possible.

The books and reference genre looks fairly popular as well, with an average number of installs of 8,767,811. It's interesting to explore this in more depth, since we found this genre has some potential to work well on the App Store, and our aim is to recommend an app genre that shows potential for being profitable on both the App Store and Google Play.

Let's take a look at some of the apps from this genre and their number of installs:

*Code:*
```
for app in android_final:
    if app[1] == 'BOOKS_AND_REFERENCE':
        print(app[0], ':', app[5])
```
*Output (as table):*
| App Name                                          | Number of Downloads     |
|---------------------------------------------------|-------------------------|
| E-Book Read - Read Book for free                  | 50,000+                 |
| Download free book with green book                | 100,000+                |
| Wikipedia                                         | 10,000,000+             |
| Cool Reader                                       | 10,000,000+             |
| Free Panda Radio Music                            | 100,000+                |
| Book store                                        | 1,000,000+              |
| FBReader: Favorite Book Reader                    | 10,000,000+             |
| English Grammar Complete Handbook                 | 500,000+                |
| Free Books - Spirit Fanfiction and Stories        | 1,000,000+              |
| Google Play Books                                 | 1,000,000,000+          |
| AlReader -any text book reader                    | 5,000,000+              |
| Offline English Dictionary                        | 100,000+                |
| Offline: English to Tagalog Dictionary            | 500,000+                |
| FamilySearch Tree                                 | 1,000,000+              |
| Cloud of Books                                    | 1,000,000+              |
| Recipes of Prophetic Medicine for free            | 500,000+                |
| ReadEra – free ebook reader                       | 1,000,000+              |
| Anonymous caller detection                        | 10,000+                 |
| Ebook Reader                                     | 5,000,000+              |
| Litnet - E-books                                  | 100,000+                |
| Read books online                                 | 5,000,000+              |
| English to Urdu Dictionary                        | 500,000+                |
| eBoox: book reader fb2 epub zip                   | 1,000,000+              |
| English Persian Dictionary                        | 500,000+                |
| Flybook                                           | 500,000+                |
| All Maths Formulas                                | 1,000,000+              |
| Ancestry                                         | 5,000,000+              |
| HTC Help                                         | 10,000,000+             |
| English translation from Bengali                  | 100,000+                |
| Pdf Book Download - Read Pdf Book                 | 100,000+                |
| Free Book Reader                                 | 100,000+                |
| eBoox new: Reader for fb2 epub zip books          | 50,000+                 |
| Only 30 days in English, the guideline is guaranteed | 500,000+             |
| Moon+ Reader                                     | 10,000,000+             |
| SH-02J Owner's Manual (Android 8.0)               | 50,000+                 |
| English-Myanmar Dictionary                        | 1,000,000+              |
| Golden Dictionary (EN-AR)                         | 1,000,000+              |
| All Language Translator Free                      | 1,000,000+              |
| Azpen eReader                                    | 500,000+                |
| URBANO V 02 instruction manual                    | 100,000+                |
| Bible                                            | 100,000,000+            |
| C Programs and Reference                         | 50,000+                 |
| C Offline Tutorial                               | 1,000+                  |
| C Programs Handbook                              | 50,000+                 |
| Amazon Kindle                                    | 100,000,000+            |
| Aab e Hayat Full Novel                           | 100,000+                |
| Aldiko Book Reader                               | 10,000,000+             |
| Google I/O 2018                                  | 500,000+                |
| R Language Reference Guide                       | 10,000+                 |
| Learn R Programming Full                         | 5,000+                  |
| R Programing Offline Tutorial                    | 1,000+                  |
| Guide for R Programming                          | 5+                      |
| Learn R Programming                              | 10+                     |
| R Quick Reference Big Data                       | 1,000+                  |
| V Made                                           | 100,000+                |
| Wattpad 📖 Free Books                            | 100,000,000+            |
| Dictionary - WordWeb                             | 5,000,000+              |
| Guide (for X-MEN)                                | 100,000+                |
| AC Air condition Troubleshoot,Repair,Maintenance  | 5,000+                  |
| AE Bulletins                                     | 1,000+                  |
| Ae Allah na Dai (Rasa)                           | 10,000+                 |
| 50000 Free eBooks & Free AudioBooks              | 5,000,000+              |
| Ag PhD Field Guide                               | 10,000+                 |
| Ag PhD Deficiencies                              | 10,000+                 |
| Ag PhD Planting Population Calculator            | 1,000+                  |
| Ag PhD Soybean Diseases                          | 1,000+                  |
| Fertilizer Removal By Crop                       | 50,000+                 |
| A-J Media Vault                                  | 50+                     |
| Al-Quran (Free)                                  | 10,000,000+             |
| Al Quran (Tafsir & by Word)                      | 500,000+                |
| Al Quran Indonesia                               | 10,000,000+             |
| Al'Quran Bahasa Indonesia                        | 10,000,000+             |
| Al Quran Al karim                                | 1,000,000+              |
| Al-Muhaffiz                                      | 50,000+                 |
| Al Quran : EAlim - Translations & MP3 Offline    | 5,000,000+              |
| Al-Quran 30 Juz free copies                      | 500,000+                |
| Koran Read &MP3 30 Juz Offline                   | 1,000,000+              |
| Hafizi Quran 15 lines per page                   | 1,000,000+              |
| Quran for Android                                | 10,000,000+             |
| Surah Al-Waqiah                                  | 100,000+                |
| Hisnul Al Muslim - Hisn Invocations & Adhkaar    | 100,000+                |
| Satellite AR                                     | 1,000,000+              |
| Audiobooks from Audible                          | 100,000,000+            |
| Kinot & Eichah for Tisha B'Av                    | 10,000+                 |
| AW Tozer Devotionals - Daily                     | 5,000+                  |
| Tozer Devotional -Series 1                       | 1,000+                  |
| The Pursuit of God                               | 1,000+                  |
| AY Sing                                          | 5,000+                  |
| Ay Hasnain k Nana Milad Naat                     | 10,000+                 |
| Ay Mohabbat Teri Khatir Novel                    | 10,000+                 |
| Arizona Statutes, ARS (AZ Law)                   | 1,000+                  |
| Oxford A-Z of English Usage                      | 


The book and reference genre includes a variety of apps: software for processing and reading ebooks, various collections of libraries, dictionaries, tutorials on programming or languages, etc. It seems there's still a small number of extremely popular apps that skew the average:

*Code:*
```
for app in android_final:
    if app[1] == 'BOOKS_AND_REFERENCE' and (app[5] == '1,000,000,000+'
                                            or app[5] == '500,000,000+'
                                            or app[5] == '100,000,000+'):
        print(app[0], ':', app[5])
```
*Output (as table):*
| Platform                       | Number of Downloads   |
|--------------------------------|----------------------|
| Google Play Books              | 1,000,000,000+       |
| Bible                          | 100,000,000+         |
| Amazon Kindle                  | 100,000,000+         |
| Wattpad 📖 Free Books           | 100,000,000+         |
| Audiobooks from Audible        | 100,000,000+         |

However, it looks like there are only a few very popular apps, so this market still shows potential. Let's try to get some app ideas based on the kind of apps that are somewhere in the middle in terms of popularity (between 1,000,000 and 100,000,000 downloads):

*Code:*
```
for app in android_final:
    if app[1] == 'BOOKS_AND_REFERENCE' and (app[5] == '1,000,000+'
                                            or app[5] == '5,000,000+'
                                            or app[5] == '10,000,000+'
                                            or app[5] == '50,000,000+'):
        print(app[0], ':', app[5])
```
*Output (as tabel):*
| App Name                                         | Number of Downloads   |
|--------------------------------------------------|----------------------|
| Wikipedia                                        | 10,000,000+          |
| Cool Reader                                      | 10,000,000+          |
| Book store                                       | 1,000,000+           |
| FBReader: Favorite Book Reader                   | 10,000,000+          |
| Free Books - Spirit Fanfiction and Stories       | 1,000,000+           |
| AlReader - any text book reader                  | 5,000,000+           |
| FamilySearch Tree                                | 1,000,000+           |
| Cloud of Books                                   | 1,000,000+           |
| ReadEra – free ebook reader                      | 1,000,000+           |
| Ebook Reader                                     | 5,000,000+           |
| Read books online                                | 5,000,000+           |
| eBoox: book reader fb2 epub zip                  | 1,000,000+           |
| All Maths Formulas                               | 1,000,000+           |
| Ancestry                                         | 5,000,000+           |
| HTC Help                                         | 10,000,000+          |
| Moon+ Reader                                     | 10,000,000+          |
| English-Myanmar Dictionary                       | 1,000,000+           |
| Golden Dictionary (EN-AR)                        | 1,000,000+           |
| All Language Translator Free                     | 1,000,000+           |
| Aldiko Book Reader                               | 10,000,000+          |
| Dictionary - WordWeb                             | 5,000,000+           |
| 50000 Free eBooks & Free AudioBooks              | 5,000,000+           |
| Al-Quran (Free)                                  | 10,000,000+          |
| Al Quran Indonesia                               | 10,000,000+          |
| Al'Quran Bahasa Indonesia                        | 10,000,000+          |
| Al Quran Al karim                                | 1,000,000+           |
| Al Quran: EAlim - Translations & MP3 Offline     | 5,000,000+           |
| Koran Read &MP3 30 Juz Offline                   | 1,000,000+           |
| Hafizi Quran 15 lines per page                   | 1,000,000+           |
| Quran for Android                                | 10,000,000+          |
| Satellite AR                                     | 1,000,000+           |
| Oxford A-Z of English Usage                      | 1,000,000+           |
| Dictionary.com: Find Definitions for English Words | 10,000,000+        |
| English Dictionary - Offline                     | 10,000,000+          |
| Bible KJV                                        | 5,000,000+           |
| NOOK: Read eBooks & Magazines                    | 10,000,000+          |
| Brilliant Quotes: Life, Love, Family & Motivation | 1,000,000+           |
| Stats Royale for Clash Royale                    | 1,000,000+           |
| Dictionary                                       | 10,000,000+          |
| wikiHow: how to do anything                      | 1,000,000+           |
| EGW Writings                                     | 1,000,000+           |
| My Little Pony AR Guide                          | 1,000,000+           |
| Spanish English Translator                       | 10,000,000+          |
| Dictionary - Merriam-Webster                     | 10,000,000+          |
| JW Library                                       | 10,000,000+          |
| Oxford Dictionary of English : Free              | 10,000,000+          |
| English Hindi Dictionary                         | 10,000,000+          |
| English to Hindi Dictionary                      | 5,000,000+           |


This niche seems to be dominated by software for processing and reading ebooks, as well as various collections of libraries and dictionaries, so it's probably not a good idea to build similar apps since there'll be some significant competition.

We also notice there are quite a few apps built around the book Quran, which suggests that building an app around a popular book can be profitable. It seems that taking a popular book (perhaps a more recent book) and turning it into an app could be profitable for both the Google Play and the App Store markets.

However, it looks like the market is already full of libraries, so we need to add some special features besides the raw version of the book. This might include daily quotes from the book, an audio version of the book, quizzes on the book, a forum where people can discuss the book, etc.



## Conclusion

In this project, we analyzed data about the App Store and Google Play mobile apps with the goal of recommending an app profile that can be profitable for both markets.

We concluded that taking a popular book (perhaps a more recent book) and turning it into an app could be profitable for both the Google Play and the App Store markets. The markets are already full of libraries, so we need to add some special features besides the raw version of the book. This might include daily quotes from the book, an audio version of the book, quizzes on the book, a forum where people can discuss the book, etc


## Contact
I am **Athar Imran** a Data Scientist with a passion for using data to solve real-world problems.  I am proficient in Python, and I am always eager to learn more about data science and machine learning. I am a creative thinker and a problem solver, and  I am always looking for new ways to use my skills in Python to solve real-world problems.. I am looking for opportunities to use my skills and knowledge to make a positive impact on the world.

You can find me at [Twitter](https://twitter.com/atharimran728), [Github](https://github.com/AtharImran728) and [atharimran728@gmail.com](mailto:atharimran728@email.com)