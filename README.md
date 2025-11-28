<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: English Expressions</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: English Expressions</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>almost</h3>
                    <p><strong>Definition:</strong> Very nearly; not quite.</p>
                    <p><strong>Usage:</strong> Used to indicate that something is very close to happening or being true.</p>
                    <p class="example"><strong>Example:</strong> "I almost missed the bus this morning."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>town</h3>
                    <p><strong>Definition:</strong> An urban area that is larger than a village but smaller than a city.</p>
                    <p><strong>Usage:</strong> Refers to a populated area with its own local government.</p>
                    <p class="example"><strong>Example:</strong> "She lives in a small town in the countryside."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>times (volte)</h3>
                    <p><strong>Definition:</strong> Instances or occasions; used to indicate frequency.</p>
                    <p><strong>Usage:</strong> Refers to how many times something happens.</p>
                    <p class="example"><strong>Example:</strong> "I've visited Paris three times."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>way back (ritorno)</h3>
                    <p><strong>Definition:</strong> The return journey; coming back from somewhere.</p>
                    <p><strong>Usage:</strong> Refers to the trip returning to the starting point.</p>
                    <p class="example"><strong>Example:</strong> "The way back home seemed longer than the trip there."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>toll (pedaggio)</h3>
                    <p><strong>Definition:</strong> A charge payable for permission to use a particular road or bridge.</p>
                    <p><strong>Usage:</strong> Refers to fees paid for using certain roads or infrastructure.</p>
                    <p class="example"><strong>Example:</strong> "We had to pay a toll to cross the bridge."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>dark</h3>
                    <p><strong>Definition:</strong> With little or no light; not light in color.</p>
                    <p><strong>Usage:</strong> Describes absence of light or deep colors.</p>
                    <p class="example"><strong>Example:</strong> "It gets dark early in the winter."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>slow down</h3>
                    <p><strong>Definition:</strong> To reduce speed; to become less active or intense.</p>
                    <p><strong>Usage:</strong> Can refer to physical speed or pace of activity.</p>
                    <p class="example"><strong>Example:</strong> "You should slow down when driving in bad weather."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>ferry</h3>
                    <p><strong>Definition:</strong> A boat that transports people, vehicles, or goods across a body of water.</p>
                    <p><strong>Usage:</strong> Refers to water transportation services.</p>
                    <p class="example"><strong>Example:</strong> "We took the ferry to reach the island."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>owner</h3>
                    <p><strong>Definition:</strong> A person who owns something; possessor.</p>
                    <p><strong>Usage:</strong> Refers to someone who has legal possession of property.</p>
                    <p class="example"><strong>Example:</strong> "The restaurant owner greeted us at the door."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>soil</h3>
                    <p><strong>Definition:</strong> The top layer of earth in which plants grow; ground.</p>
                    <p><strong>Usage:</strong> Refers to earth or dirt, especially for gardening or farming.</p>
                    <p class="example"><strong>Example:</strong> "The soil in this area is perfect for growing vegetables."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">almost</span>
                    <span class="word-option">town</span>
                    <span class="word-option">times</span>
                    <span class="word-option">way back</span>
                    <span class="word-option">toll</span>
                    <span class="word-option">dark</span>
                    <span class="word-option">slow down</span>
                    <span class="word-option">ferry</span>
                    <span class="word-option">owner</span>
                    <span class="word-option">soil</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="almost" onclick="selectMatch(this)">almost</div>
                    <div class="match-item" data-word="town" onclick="selectMatch(this)">town</div>
                    <div class="match-item" data-word="times" onclick="selectMatch(this)">times</div>
                    <div class="match-item" data-word="way back" onclick="selectMatch(this)">way back</div>
                    <div class="match-item" data-word="toll" onclick="selectMatch(this)">toll</div>
                    <div class="match-item" data-word="dark" onclick="selectMatch(this)">dark</div>
                    <div class="match-item" data-word="slow down" onclick="selectMatch(this)">slow down</div>
                    <div class="match-item" data-word="ferry" onclick="selectMatch(this)">ferry</div>
                    <div class="match-item" data-word="owner" onclick="selectMatch(this)">owner</div>
                    <div class="match-item" data-word="soil" onclick="selectMatch(this)">soil</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "almost" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Completely</div>
                    <div class="option" onclick="selectOption(this, true)">Very nearly; not quite</div>
                    <div class="option" onclick="selectOption(this, false)">Far from</div>
                    <div class="option" onclick="selectOption(this, false)">Exactly</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What is a "town"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A very large city</div>
                    <div class="option" onclick="selectOption(this, true)">An urban area larger than a village but smaller than a city</div>
                    <div class="option" onclick="selectOption(this, false)">A rural farm area</div>
                    <div class="option" onclick="selectOption(this, false)">A body of water</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "times" mean in the context of "volte"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Mathematical multiplication</div>
                    <div class="option" onclick="selectOption(this, true)">Instances or occasions; frequency</div>
                    <div class="option" onclick="selectOption(this, false)">Historical periods</div>
                    <div class="option" onclick="selectOption(this, false)">Newspaper names</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What does "way back" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">The journey to a destination</div>
                    <div class="option" onclick="selectOption(this, true)">The return journey; coming back</div>
                    <div class="option" onclick="selectOption(this, false)">A difficult path</div>
                    <div class="option" onclick="selectOption(this, false)">A memory from long ago</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What is a "toll"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of bell</div>
                    <div class="option" onclick="selectOption(this, true)">A charge for using a road or bridge</div>
                    <div class="option" onclick="selectOption(this, false)">A tall building</div>
                    <div class="option" onclick="selectOption(this, false)">A type of tax</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "dark" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Very bright</div>
                    <div class="option" onclick="selectOption(this, true)">With little or no light</div>
                    <div class="option" onclick="selectOption(this, false)">Colorful</div>
                    <div class="option" onclick="selectOption(this, false)">Transparent</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What does "slow down" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To speed up</div>
                    <div class="option" onclick="selectOption(this, true)">To reduce speed; become less active</div>
                    <div class="option" onclick="selectOption(this, false)">To stop completely</div>
                    <div class="option" onclick="selectOption(this, false)">To go backwards</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What is a "ferry"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of airplane</div>
                    <div class="option" onclick="selectOption(this, true)">A boat that transports people or vehicles across water</div>
                    <div class="option" onclick="selectOption(this, false)">A train</div>
                    <div class="option" onclick="selectOption(this, false)">A bus</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: Who is an "owner"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A person who rents something</div>
                    <div class="option" onclick="selectOption(this, true)">A person who possesses something legally</div>
                    <div class="option" onclick="selectOption(this, false)">A person who borrows something</div>
                    <div class="option" onclick="selectOption(this, false)">A person who sells something</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What is "soil"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of rock</div>
                    <div class="option" onclick="selectOption(this, true)">The top layer of earth where plants grow</div>
                    <div class="option" onclick="selectOption(this, false)">A building material</div>
                    <div class="option" onclick="selectOption(this, false)">A type of water</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "almost", text: "Very nearly; not quite" },
            { meaning: "town", text: "An urban area larger than a village but smaller than a city" },
            { meaning: "times", text: "Instances or occasions; frequency" },
            { meaning: "way back", text: "The return journey; coming back" },
            { meaning: "toll", text: "A charge for using a road or bridge" },
            { meaning: "dark", text: "With little or no light" },
            { meaning: "slow down", text: "To reduce speed; become less active" },
            { meaning: "ferry", text: "A boat that transports people or vehicles across water" },
            { meaning: "owner", text: "A person who possesses something legally" },
            { meaning: "soil", text: "The top layer of earth where plants grow" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "I <input type='text' class='fill-blank' data-answer='almost' placeholder='answer'> missed the bus this morning.", answer: "almost" },
            { text: "She lives in a small <input type='text' class='fill-blank' data-answer='town' placeholder='answer'> in the countryside.", answer: "town" },
            { text: "I've visited Paris three <input type='text' class='fill-blank' data-answer='times' placeholder='answer'>.", answer: "times" },
            { text: "The <input type='text' class='fill-blank' data-answer='way back' placeholder='answer'> home seemed longer than the trip there.", answer: "way back" },
            { text: "We had to pay a <input type='text' class='fill-blank' data-answer='toll' placeholder='answer'> to cross the bridge.", answer: "toll" },
            { text: "It gets <input type='text' class='fill-blank' data-answer='dark' placeholder='answer'> early in the winter.", answer: "dark" },
            { text: "You should <input type='text' class='fill-blank' data-answer='slow down' placeholder='answer'> when driving in bad weather.", answer: "slow down" },
            { text: "We took the <input type='text' class='fill-blank' data-answer='ferry' placeholder='answer'> to reach the island.", answer: "ferry" },
            { text: "The restaurant <input type='text' class='fill-blank' data-answer='owner' placeholder='answer'> greeted us at the door.", answer: "owner" },
            { text: "The <input type='text' class='fill-blank' data-answer='soil' placeholder='answer'> in this area is perfect for growing vegetables.", answer: "soil" },
            { text: "He's called me five <input type='text' class='fill-blank' data-answer='times' placeholder='answer'> today.", answer: "times" },
            { text: "The car's <input type='text' class='fill-blank' data-answer='owner' placeholder='answer'> reported it stolen to the police.", answer: "owner" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
