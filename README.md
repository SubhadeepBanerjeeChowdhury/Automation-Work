'''
from fuzzywuzzy import fuzz

sheet_names = ["BLT Mgmt", "ChelseaGroton", "Chelsea Groton Bank", "Aurora P"]
groups = ["Aurora Productions INC", "BLT Management Inc", 'Chelsea Groton Bank Inc', 'Aurroras Productions']

# Define the fuzzy matching methods to be used
matching_methods = ['partial_ratio', 'token_set_ratio', 'ratio', 'token_sort_ratio', 'WRatio', 'partial_token_sort_ratio']

# Initialize a dictionary to store the best match for each sheet name and its highest similarity score across all methods
best_matches = {}

# Iterate through each sheet name
for sheet_name in sheet_names:
    # Initialize variables to store the best match and its highest similarity score
    best_match = None
    best_score = 0
    
    # Iterate through each group to find the best match using all matching methods
    for group in groups:
        # Initialize variable to store the highest score among all methods for the current group
        group_best_score = 0
        
        # Iterate through each matching method
        for method in matching_methods:
            # Calculate the similarity score between the sheet name and group using the current method
            score = getattr(fuzz, method)(sheet_name.lower(), group.lower())
            
            # Update the highest score for the current group if the current score is higher
            group_best_score = max(group_best_score, score)
        
        # Update best match and its score if the current group's highest score is higher than the overall best score
        if group_best_score > best_score:
            best_match = group
            best_score = group_best_score
    
    # Save the best match and its highest score in the dictionary
    best_matches[sheet_name] = {'group': best_match, 'score': best_score}

# Print the results
for sheet_name, match_info in best_matches.items():
    print(f"Sheet name: {sheet_name}, Best match: {match_info['group']}, Highest similarity score: {match_info['score']}")

'''
