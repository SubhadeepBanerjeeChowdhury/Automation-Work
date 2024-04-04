best_matches = {}

#Iterate through each sheet name
for sheet_name in sheet_names:
    #Initialize variables to store the best match and its similarity score
    best_match = None
    best_score = 0
    
    # Iterate through each group to find the best match
    for group in groups:
        # Calculate the similarity score between the sheet name and group
        score = fuzz.ratio(sheet_name.lower(), group.lower())
        
        # Update best match if the current score is higher
        if score > best_score:
            best_match = group
            best_score = score
    
    # Save the best match and its score in the dictionary
    best_matches[sheet_name] = {'group': best_match, 'score': best_score}

# Print the results
for sheet_name, match_info in best_matches.items():
    print(f"Sheet name: {sheet_name}, Best match: {match_info['group']}, Similarity score: {match_info['score']}")
