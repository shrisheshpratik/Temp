 // Define regex pattern to match <Image> tags and content
        
        String regex = "<Image>.*?</Image>";
        
        // Compile the regex pattern
        Pattern pattern = Pattern.compile(regex, Pattern.DOTALL);
        Matcher matcher = pattern.matcher(input);
        
        // List to hold the result sections
        List<String> results = new ArrayList<>();
        
        // Track the start position of the last match
        int lastIndex = 0;

        // Extract and store sections based on <Image> tags
        while (matcher.find()) {
            // Append section before the current <Image> tag
            if (lastIndex < matcher.start()) {
                results.add(input.substring(lastIndex, matcher.start()));
            }
            // Append the current <Image> tag and its content
            results.add(matcher.group());
            // Update the last index to the end of the current <Image> tag
            lastIndex = matcher.end();
        }
        
        // Append the remaining part of the string after the last <Image> tag
        if (lastIndex < input.length()) {
            results.add(input.substring(lastIndex));
        }
