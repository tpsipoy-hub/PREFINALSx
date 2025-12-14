DISPATCH DECISION ENGINE DOCUMENTATION
Introduction
The Dispatch Decision Engine is a C++ program that adapts Episode 1 of Dispatch into a text based visual novel. The program follows Robert Robertson as he transitions from frontline superhero to dispatcher. The narrative is divided into five decision points, each implemented as a separate function. User input determines the flow of the story, updates global variables, and influences the customized epilogue.
bool isMerciful = false;            // Tracks Robert's moral path
int Blazer_Impression_Score = 0;    // Blonde Blazer’s perception of Robert
bool isRomanticTensionActive = false; // Romance route flag
int Tactical_Efficiency = 0;        // Tracks tactical success
bool gameOver = false;              // Ends story if Robert fails

Functions and Code Snippets
1. Scene 1 — Apartment Interrogation
void scene_interrogation() {
    int c = get_choice("Robert must decide:",
                       "Pull him back",
                       "Let him drop");
    if (c == 1) {
        isMerciful = true;
    } else {
        isMerciful = false;
    }
}
Decision Path:
•	Pull Him Back → Robert shows compassion (isMerciful = true).
•	Let Him Drop → Robert shows ruthless efficiency (isMerciful = false).

2. Scene 2 — Street Fight
void scene_street_fight() {
    int c = get_choice("Robert must act:",
                       "Right hand punch",
                       "Left hand punch");
    if (c == 1) {
        gameOver = true;
    } else {
        Tactical_Efficiency += 2;
    }
}

Decision Path:
•	Right Hand Punch → Failure, sets gameOver = true.
•	Left Hand Punch → Success, increases Tactical_Efficiency.
3. Scene 3 — Superhero Bar Scene

void scene_bar_flambae() {
    int c = get_choice("Robert must choose:",
                       "Throw water",
                       "Throw alcohol");
    if (c == 1) {
        Blazer_Impression_Score += 1;
    } else {
        Blazer_Impression_Score += 3;
    }
}
Decision Path:
•	Throw Water → Subdued outcome, small impression gain.
•	Throw Alcohol → Chaotic spectacle, stronger impression remembered by Blonde Blazer.
4. Scene 4 — Billboard Romance
void scene_billboard() {
    int c = get_choice("Robert must decide:",
                       "Choose to kiss",
                       "Let the moment pass");
    if (c == 1) {
        isRomanticTensionActive = true;
        Blazer_Impression_Score += 2;
    } else {
        isRomanticTensionActive = true;
        Blazer_Impression_Score += 1;
    }
}
Decision Path:
•	Kiss → Romance route unlocked, stronger impression.
•	Let Moment Pass → Romance tension remains, smaller impression.

5. Scene 5 — Combat vs Toxic
void scene_combat_toxic() {
    int c = get_choice("Robert must choose:",
                       "Punt",
                       "Stomp");
    if (c == 1) {
        Tactical_Efficiency += (isMerciful ? 2 : 1);
    } else {
        Tactical_Efficiency += (isMerciful ? 1 : 2);
    }
}

Decision Path:
•	Punt → Flashy, creative, comic relief. Efficiency bonus if merciful.
•	Stomp → Brutal efficiency, intimidation. Efficiency bonus if ruthless.
Epilogue — Summary

void epilogue_summary() {
    if (isMerciful) {
        cout << "Robert is remembered for compassionate leadership.";
    } else {
        cout << "Robert is remembered for pragmatic efficiency.";
    }
}

Decision Path:
•	Epilogue integrates all variables (isMerciful, Blazer_Impression_Score, isRomanticTensionActive, Tactical_Efficiency) to produce a customized ending.

