 // Define regex pattern to match <Image> tags and content
        
        String regex = "(<Image>.*?</Image>)|(<[^>]+>.*?</[^>]+>)";

        // Compile the regex pattern
        Pattern pattern = Pattern.compile(regex, Pattern.DOTALL);

        // Create a matcher for the input string
        Matcher matcher = pattern.matcher(input);

        // List to hold the results
        List<String> results = new ArrayList<>();

        // Keep track of the end of the last match
        int lastEnd = 0;

        // Find and add the matches to the list
        while (matcher.find()) {
            // Add the content between the last match and the current match
            if (matcher.start() > lastEnd) {
                results.add(input.substring(lastEnd, matcher.start()));
            }
            // Add the current match
            results.add(matcher.group());
            // Update the last end position
            lastEnd = matcher.end();
        }

        // Add the remaining part of the string after the last match
        if (lastEnd < input.length()) {
            results.add(input.substring(lastEnd));
        }
