# Users Journery Analaysis



## Documentation

[preprocessing_.ipynb](https://github.com/phinglaspure123/User-Journery-Analysis/blob/main/preprocessing_.ipynb)

This file is used for preprocessing the raw data
 
(user_journery_raw.csv) => (clean_data.csv)

#### Functions Used
- group_data 
     - This function aggregates user journeys based on the specified session parameter and groups by group_column (default is user_id).
    - session: Determines which part of the user journey to consider.
    - 'all': Takes the entire user journey.
    - 'all_except_last': Excludes the last entry.
    - 'Last': Takes the last specified number of entries.
    - 'first': Takes the first specified number of entries.
    - group_mask: A boolean mask used to filter rows for a specific group.
    - user_journey: Aggregates the user journey entries into a single string.
    - empty_df: Stores the aggregated results.

- remove_pages
    - This function removes specified pages (actions) from user journeys.
    - pages: A list of pages to be removed.
    - It splits each journey string into a list of pages, filters out unwanted pages, and then joins them back into a string.
    - clean_data: Applies the remove_pages function with an empty  list of pages (no pages removed in this case).

- remove_page_duplicates
    - This function removes consecutive duplicate pages in each user journey.
    - It splits each journey into a list of pages, checks for consecutive duplicates, and removes them.
    - clean_data: Applies the remove_page_duplicates function to clean the DataFrame.

[analysis_.ipynb](https://github.com/phinglaspure123/User-Journery-Analysis/blob/main/analysis_.ipynb)

This Notebook is used for Analysis of the user_journey from the clean_data.csv which was created above

To understand the behavior of users based on their subscription types, we will analyze their journey through various pages.

#### Functions Used

- filter_vai_subcription
    - Purpose: To filter the dataset based on the subscription type.
    - Parameters:
        - data: The dataset to be filtered.
        - filter: The subscription type to filter by (e.g., 'Annual', 'Monthly'). Defaults to "all" which means no filtering.
        - target_column: The column in the dataset that indicates the subscription type. Defaults to 'subscription_type'.

    -   Functionality:
        - If filter is set to "all", it returns the entire dataset without filtering.
        - Otherwise, it filters the dataset to include only rows where the target_column matches the specified filter value.

- split_user_journey
    - Purpose: To split the user journey strings into lists of individual pages.
    - Parameters:
        - data: The dataset containing user journeys.
        - target_column: The column that holds the user journey as a string. Defaults to 'user_journey'.
    - Functionality:
        - It splits the strings in the target_column on the "-" character, converting them into lists of pages.
        - This is useful for subsequent analysis where each page in the journey needs to be considered separately.

- page_count
    - Purpose: To count the occurrences of each page in the user journeys.
    - Parameters:
        - data: The dataset containing user journeys.
        - target_column: The column containing the user journeys as lists of pages. Defaults to 'user_journey'.
        - subcription_type: The type of subscription to filter by before counting pages. Defaults to 'all'.
        - sort: A boolean indicating whether to sort the counts in ascending order. Defaults to False (descending order).
    - Functionality:
        - It first filters the data based on the specified subcription_type.
        - Then, it flattens all user journeys into a single list of pages and counts the occurrences of each page.
        - Finally, it creates a DataFrame from these counts, optionally sorting them, and returns it.


- page_presence
    - Purpose: To count the presence of each page across all user journeys.
    - Parameters:
        - data: The dataset containing user journeys.
        - target_column: The column containing the user journeys as lists of pages. Defaults to 'user_journey'.
        - subcription_type: The type of subscription to filter by before counting page presence. Defaults to 'all'.
        - sort: A boolean indicating whether to sort the presence counts in ascending order. Defaults to False (descending order).
    - Functionality:
        - It filters the data based on the specified subcription_type.
        - Converts each user journey to a set (to avoid counting duplicate pages within a single journey).
        - Counts the presence of each page across all journeys.
        - Creates and returns a DataFrame with the counts, optionally sorted, including the total number of journeys.

- page_destination
    - Purpose: To analyze the transitions between pages in user journeys.
    - Parameters:
        - data: The dataset containing user journeys.
        - target_column: The column containing the user journeys as lists of pages. Defaults to 'user_journey'.
        - subcription_type: The type of subscription to filter by before analyzing transitions. Defaults to 'all'.
        - sort: A boolean indicating whether to sort the transitions in ascending order. Defaults to False (descending order).
    - Functionality:
        - It filters the data based on the specified subcription_type.
        - Iterates through each journey to record the transitions from one page to the next.
        - Counts how often each transition (from one page to the next) occurs.
        - Returns a dictionary where each page maps to another dictionary showing the counts of transitions to subsequent pages, optionally sorted.

- page_sequence
    - Purpose: To analyze sequences of pages of a specified length within user journeys.
    - Parameters:
        - data: The dataset containing user journeys.
        - target_column: The column containing the user journeys as lists of pages. Defaults to 'user_journey'.
        - sequence: The length of the page sequence to analyze. Defaults to 3.
        - subcription_type: The type of subscription to filter by before analyzing sequences. Defaults to 'all'.
        - sort: A boolean indicating whether to sort the sequence counts in ascending order. Defaults to False (descending order).
    -  Functionality:
        - It filters the data based on the specified subcription_type.
        - Extracts all possible sequences of the specified length from each user journey.
        - Counts the occurrences of each sequence.
        - Uses a flag to ensure that each sequence is only counted once per journey.
        - Returns a sorted dictionary of these sequences and their counts.

#### Purpose of Creating These Functions
The purpose of these functions is to provide a detailed analysis of user behavior on a website or platform. By filtering and analyzing user journeys based on subscription types, these functions help in understanding:

- Which pages are most frequently visited (page_count).
- How often each page appears in user journeys (page_presence).
- The most common transitions between pages (page_destination).
- Frequent sequences of pages users navigate through (page_sequence).
## Authors

- [@ Pushpak Hinglaspure](https://github.com/phinglaspure123)

