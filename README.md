//efsnf



        // Regular expression to match <image> tags and their content
        List<String> sections = new ArrayList<>();
        String regex = "<image.*?>.*?</image>";
        Pattern pattern = Pattern.compile(regex, Pattern.DOTALL);
        Matcher matcher = pattern.matcher(input);
        
        int lastIndex = 0;
        
        // Extract sections before, between, and after <image> tags
        while (matcher.find()) {
            // Add section before the current <image> tag
            if (matcher.start() > lastIndex) {
                sections.add(input.substring(lastIndex, matcher.start()));
            }

            // Add section containing the current <image> tag
            sections.add(matcher.group());

            lastIndex = matcher.end();
        }

        // Add section after the last <image> tag
        if (lastIndex < input.length()) {
            sections.add(input.substring(lastIndex));
        }
        
        return sections;
