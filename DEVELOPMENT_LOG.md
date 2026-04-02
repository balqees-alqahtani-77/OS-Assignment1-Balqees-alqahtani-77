# Development Log

## Instructions
Document your development process as you work on the assignment. Add entries showing:
- What you worked on
- Problems you encountered
- How you solved them
- Time spent

**Requirements**: Minimum 5 entries showing progression over time.

---

## Example Entry Format:

### Entry 1 - [April 1, 2026, 2:30 PM]
**What I did**: Forked the repository and set up my student ID

**Details**: 
- Created GitHub account with university email
- Forked the starter repository
- Changed student ID on line 92 to my actual ID (441234567)
- Compiled and ran the program successfully

**Challenges**: Had to install JDK first because javac wasn't recognized

**Solution**: Downloaded JDK 17 from Oracle website and set PATH variable

**Time spent**: 30 minutes

---

## Your Development Log:
Entry 1 - March 20, 2026 (9:00 PM - 10:30 PM)

What I did:

· Forked the starter repository from GitHub
· Cloned the repository to my local machine using VS Code
· Set up my development environment (VS Code with Java Extension Pack)
· Changed the student ID in SchedulerSimulation.java

Details:
First, I created a GitHub account using my university email (@std.psau.edu.sa) as required. Then I went to the professor's starter repository and clicked the "Fork" button to create my own copy. After forking, I renamed the repository from "OS-Assignment1-Starter" to "OS-Assignment1-[MyName]". I installed VS Code and cloned my forked repository. I opened SchedulerSimulation.java and changed line 92 from int studentID = 123456789; to int studentID = 445052134; (my actual student ID). I also tested that the code compiles by running javac SchedulerSimulation.java.

Challenges:

· At first, I didn't know how to clone a repository from GitHub using VS Code
· I had some issues with Java not being recognized in the terminal

Solution:

· I watched a tutorial on "VS Code GitHub integration" and learned to use the Command Palette (Ctrl+Shift+P) and search for "Git: Clone"
· I reinstalled Java JDK and added it to my system PATH

Time spent: 1.5 hours

---

Entry 2 - March 22, 2026 (7:00 PM - 9:00 PM)

What I did:

· Implemented Feature 1: Added priority field to Process class
· Generated random priorities for each process (1-5, where 5 is highest)
· Updated the output message to display priority

Details:
I added a private integer variable called priority to the Process class. I modified the Process constructor to accept a priority parameter. In the main method, I added code to generate random priority values between 1 and 5 for each process. I also updated the addProcessToQueue method to display the priority when a process enters the ready queue. The output now shows: "➕ P1 added to ready queue │ Burst time: 4500ms │ Priority: 3"

Challenges:

· I had to make sure the priority field was properly passed through the constructor
· I needed to decide where to store the priority value and how to display it

Solution:

· I added getter method getPriority() to access the priority value from outside the Process class
· I modified the print statement in addProcessToQueue to include process.getPriority()
· I tested the code multiple times to verify random priorities are generated correctly (values between 1 and 5)

Time spent: 2 hours

---

Entry 3 - March 24, 2026 (8:30 PM - 10:00 PM)

What I did:

· Implemented Feature 2: Added context switch counter
· Created static counter variable
· Incremented counter each time a new process starts running
· Displayed total context switches at the end of simulation

Details:
I added a static integer variable contextSwitchCount at the class level of SchedulerSimulation. Every time the scheduler pulls a new thread from the queue (in the main while loop), I increment this counter. At the end of the simulation, I added a new statistics section that displays: "Total Context Switches: 42". I used a nicely formatted box with colors to match the existing output style.

Challenges:

· I wasn't sure exactly where to increment the counter (before or after polling the queue)
· I had to decide whether to count the first process execution as a context switch

Solution:

· I placed the increment right after processQueue.poll() but before starting the thread, because each time we start a new process from the queue it represents a context switch
· I did NOT count the very first process as a context switch from "nothing" - only switches between processes
· I tested with different numbers of processes to verify the count makes sense (it should be equal to number of executions)

Time spent: 1.5 hours

---

Entry 4 - March 26, 2026 (6:00 PM - 8:30 PM)

What I did:

· Implemented Feature 3: Added waiting time tracking for each process
· Added fields to track creation time, last ready time, and total waiting time
· Calculated waiting time for each process when it starts executing
· Created summary table to display waiting times at the end

Details:
I added three new fields to the Process class: creationTime, totalWaitingTime, and lastReadyTime. In the constructor, I initialize creationTime and lastReadyTime using System.currentTimeMillis(). I created a method updateWaitingTime() that calculates how long the process waited since it was last added to the ready queue. When a process re-enters the queue, I call setLastReadyTime() to record the time. At the end of the simulation, I created displayWaitingTimeSummary() which shows a table with Process Name, Burst Time, Priority, and Waiting Time for each process, plus the average waiting time.

Challenges:

· Calculating waiting time correctly for processes that

### Entry 5 - [Date and Time]
**What I did**: 

**Details**: 

**Challenges**: 

**Solution**: 

**Time spent**: 

---

### Entry 6 - [Optional - Date and Time]
**What I did**: 

**Details**: 

**Challenges**: 

**Solution**: 

**Time spent**: 

---

## Summary

Total time spent on assignment: 7 hours

---

Most challenging part:

Calculating waiting time for processes that re-enter the queue multiple times. The issue was tracking when each process last entered the queue, not just when it was created. Also, coordinating all three features without breaking existing functionality.

---

Most interesting learning:

Seeing Round-Robin scheduling visually with progress bars and queue visualization helped me understand why this algorithm is popular in OS. Also learned the value of separate Git commits for each feature - made debugging much easier.

---

What I would do differently next time:

1. Start earlier - waited too long before beginning
2. Test each feature immediately after implementing it
3. Use debugger instead of print statements
4. Write comments while coding not after finishing
5. Record video in parts instead of one long take

---
