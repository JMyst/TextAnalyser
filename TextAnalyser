using System;
using System.IO;

class stringTest
{
    static void Main(string[] args)
    {
        string userString;
        bool noRepeat = true;

        do
        {
            Console.BackgroundColor = ConsoleColor.DarkBlue;
            Console.Clear();
            Console.ForegroundColor = ConsoleColor.White;
            stringTest keyboardTest = new stringTest();
            stringTest fileTest = new stringTest();
            Console.WriteLine("Enter Q to terminate the application\n\n");
            Console.WriteLine("1. Do you want to enter the text via the keyboard?\n2. Do you want to read in the text from a file?\n(enter 1 or 2 to choose)");
            userString = Console.ReadLine();

            // Ask the user which word analyser they would like to use

            switch (userString)
            {
                case "1":
                    keyboardTest.KeyboardRead();
                    noRepeat = false;
                    break;

                case "2":
                    fileTest.FileRead();
                    noRepeat = false;
                    break;

                // Default case if the user inputs the wrong value

                default:
                    continue;
            }
        }
        while (noRepeat == true);
    }

    void KeyboardRead()
    {
        // Declare values

        bool carryOn = true;
        string userTextEntry;
        int vowels = 0;
        int consonants = 0;
        int upperCase = 0;
        int lowerCase = 0;
        int freq = 0;
        int sentence = 0;

        // while loop to allow the user to use the function multiple times
        while (carryOn == true)
        {
            Console.WriteLine("\nYou are choosing to read from the keyboard, please input your desired text:");
            userTextEntry = Console.ReadLine();

            if (userTextEntry == "Q" || userTextEntry == "q")
            {

                // If the 'q' key is entered, the console application terminates

                System.Environment.Exit(-1);
            }

            foreach (char c in userTextEntry)
            {
                if (c == '.' || c == '!' || c == '?')
                {
                    // Takes note of sentence-ending punctuation which determines the sentence number
                    sentence++;
                }
                if (char.IsLetter(c))
                {
                    freq++;

                    // Checks for vowels

                    if (c == 'a' || c == 'A' || c == 'e' || c == 'E' || c == 'i' || c == 'I' || c == 'o' || c == 'O' || c == 'u' || c == 'U')
                    {
                        vowels++;
                    }
                    else
                    {
                        // If no vowels are found, it must a be consonant

                        consonants++;
                    }
                    if (char.IsUpper(c))
                    {
                        // Checks for uppercasing
                        upperCase++;
                    }
                    if (!char.IsUpper(c))
                    {
                        // Checks for lowercasing
                        lowerCase++;
                    }
                }
            }

            // Display the information to the user

            Console.WriteLine("\nNumber of sentences entered = {0}", sentence);
            Console.WriteLine("Number of vowels = {0}", vowels);
            Console.WriteLine("Number of consonants = {0}", consonants);
            Console.WriteLine("Number of upper case letters = {0}", upperCase);
            Console.WriteLine("Number of lower case letters = {0}", lowerCase);
            Console.WriteLine("Letter total = {0}\n", freq);

            // Reset the information in case the user wants to input new text

            sentence = 0;
            vowels = 0;
            consonants = 0;
            upperCase = 0;
            lowerCase = 0;
            freq = 0;

            KeyboardSentiment(userTextEntry);
        }
    }
    void KeyboardSentiment(string userTextEntry)
    {
        // Declare the word array for both text files

        string[] newWords = userTextEntry.Split(' ');

        string[] positiveWords = File.ReadAllText(@"Positive Words.txt").Split(' ');
        string[] negativeWords = File.ReadAllText(@"Negative Words.txt").Split(' ');

        // Declare and set the count variables to 0

        int newWordsCount = 0;
        int positiveWordCount = 0;
        int negativeWordCount = 0;

        // Use a for loop to scan through the array

        for (int a = 0; a < newWords.Length; a++)
        {

            newWordsCount++;

            for (int b = 0; b < positiveWords.Length; b++)
            {
                // Use the in-built 'equals' operation to locate intersecting words in each file

                if (string.Equals(newWords[a], positiveWords[b], StringComparison.OrdinalIgnoreCase))
                {
                    positiveWordCount++;
                }
            }
            for (int c = 0; c < negativeWords.Length; c++)
            {
                // Same principle but with the negative-word file

                if (string.Equals(newWords[a], negativeWords[c], StringComparison.OrdinalIgnoreCase))
                {
                    negativeWordCount++;
                }
            }
        }
        int[] d = new int[(int)char.MaxValue];


        foreach (char t in userTextEntry)
        {
            d[(int)t]++;
        }

        for (int i = 0; i < (int)char.MaxValue; i++)
        {
            if (d[i] > 0 &&
            char.IsLetterOrDigit((char)i))
            {
                // If a letter or digit is found create an array element showing the its occurence

                Console.WriteLine("Letter: {0}  Frequency: {1}",
                    (char)i,
                    d[i]);
            }
        }
        Console.WriteLine("\nThere are {0} positive words", positiveWordCount);
        Console.WriteLine("There are {0} negative words", negativeWordCount);
        if (negativeWordCount == positiveWordCount)
        {
            Console.WriteLine("The text mood is neutral");
        }
        if (negativeWordCount > positiveWordCount)
        {
            Console.WriteLine("The text mood is mostly negative");
        }
        if (negativeWordCount < positiveWordCount)
        {
            Console.WriteLine("The text mood is mostly positive");
        }
    }

    void FileRead()
    {
        int vowels = 0;
        int consonants = 0;
        int upperCase = 0;
        int lowerCase = 0;
        int freq = 0;
        int sentence = 0;
        string longWordCount = "";
        string wordSize = "";
        string textRead;

        {
            Console.WriteLine("You are choosing to read from a file\n");

            // Find and assign the file location

            textRead = File.ReadAllText(@"TextSample.txt");

            foreach (char c in textRead)
            {

                // If the character is a space, reset the wordSize variable

                if (c == ' ')
                {
                    if (wordSize.Length > 7)
                    {

                        // If the wordSize is above 7 characters, add this word to the longWordCount string

                        longWordCount = longWordCount + "   " + wordSize;
                    }

                    // Reset wordSize after the word is/isn't added so new words can be built

                    wordSize = "";
                }
                if (c == '.' || c == '!' || c == '?')
                {
                    sentence++;
                }
                if (char.IsLetter(c))
                {
                    wordSize = wordSize + c;

                    freq++;
                    if (c == 'a' || c == 'A' || c == 'e' || c == 'E' || c == 'i' || c == 'I' || c == 'o' || c == 'O' || c == 'u' || c == 'U')
                    {
                        vowels++;
                    }
                    else
                    {
                        consonants++;
                    }
                    if (char.IsUpper(c))
                    {
                        upperCase++;
                    }
                    if (!char.IsUpper(c))
                    {
                        lowerCase++;
                    }
                }
            }
            Console.WriteLine("Number of sentences entered = {0}", sentence);
            Console.WriteLine("Number of vowels = {0}", vowels);
            Console.WriteLine("Number of consonants = {0}", consonants);
            Console.WriteLine("Number of upper case letters = {0}", upperCase);
            Console.WriteLine("Number of lower case letters = {0}", lowerCase);
            Console.WriteLine("Letter total = {0}\n", freq);
        }

        int[] d = new int[(int)char.MaxValue];


        foreach (char t in textRead)
        {
            d[(int)t]++;
        }

        for (int i = 0; i < (int)char.MaxValue; i++)
        {
            if (d[i] > 0 &&
            char.IsLetterOrDigit((char)i))
            {
                Console.WriteLine("Letter: {0}  Frequency: {1}",
                    (char)i,
                    d[i]);
            }
        }

        // All the words added to the longWordCount variable are then displayed in a .txt document

        File.WriteAllText(@"LongWords.txt", longWordCount);

        FileSentiment(textRead);
    }

    void FileSentiment(string textRead)
    {
        string[] newWords = textRead.Split(' ');

        string[] positiveWords = File.ReadAllText(@"Positive Words.txt").Split(' ');
        string[] negativeWords = File.ReadAllText(@"Negative Words.txt").Split(' ');

        int newWordsCount = 0;
        int positiveWordCount = 0;
        int negativeWordCount = 0;

        for (int a = 0; a < newWords.Length; a++)
        {
            newWordsCount++;

            for (int b = 0; b < positiveWords.Length; b++)
            {
                if (string.Equals(newWords[a], positiveWords[b], StringComparison.OrdinalIgnoreCase))
                {
                    positiveWordCount++;
                }
            }
            for (int c = 0; c < negativeWords.Length; c++)
            {
                if (string.Equals(newWords[a], negativeWords[c], StringComparison.OrdinalIgnoreCase))
                {
                    negativeWordCount++;
                }
            }

        }

        Console.WriteLine("\nThere are {0} positive words", positiveWordCount);
        Console.WriteLine("There are {0} negative words", negativeWordCount);

        if (negativeWordCount == positiveWordCount)
        {
            Console.WriteLine("The text mood is neutral");
        }
        if (negativeWordCount > positiveWordCount)
        {
            Console.WriteLine("The text mood is mostly negative");
        }
        if (negativeWordCount < positiveWordCount)
        {
            Console.WriteLine("The text mood is mostly positive");
        }

        string inputKey = Console.ReadKey().Key.ToString();
        if (inputKey == "Q" || inputKey == "q")
        {
            System.Environment.Exit(-1);
        }

    }
}
