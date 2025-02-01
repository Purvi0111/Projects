# Task 1 : 
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main() {
    // Seed the random number generator
    srand(time(0));

    // Generate a random number between 1 and 100
    int secretNumber = rand() % 100 + 1;
    int guess;

    cout << "I've chosen a random number between 1 and 100. Can you guess it?" << endl;

    do {
        cout << "Enter your guess: ";
        cin >> guess;

        if (guess < secretNumber) {
            cout << "Too low!" << endl;
        } else if (guess > secretNumber) {
            cout << "Too high!" << endl;
        } else {
            cout << "Congratulations! You guessed the number." << endl;
        }
    } while (guess != secretNumber);

    return 0;
}

# Task 2 :
#include <iostream>

using namespace std;

int main() {
    double num1, num2;
    char operation;

cout << "Enter the first number: ";
    cin >> num1;

    cout << "Enter the second number: ";
    cin >> num2;

    cout << "Choose an operation (+, -, *, /): ";
    cin >> operation;

    switch (operation) {
        case '+':
            cout << "Result: " << num1 + num2 << endl;
            break;
        case '-':
            cout << "Result: " << num1 - num2 << endl;
            break;
        case '*':
            cout << "Result: " << num1 * num2 << endl;
            break;
        case '/':
            if (num2 == 0) {
                cout << "Error: Division by zero is not allowed." << endl;
            } else {
                cout << "Result: " << num1 / num2 << endl;
            }
            break;
        default:
            cout << "Invalid operation." << endl;
    }

    return 0;
}

# Task 3 : 
#include <iostream>

using namespace std;

char board[3][3] = {{' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '}};
char currentPlayer = 'X';

void displayBoard() {
    cout << "-------------" << endl;
    for (int i = 0; i < 3; i++) {
        cout << "| ";
        for (int j = 0; j < 3; j++) {
            cout << board[i][j] << " | ";
        }
        cout << endl << "-------------" << endl;
    }
}

bool checkWin() {
    // Check rows
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == currentPlayer && board[i][1] == currentPlayer && board[i][2] == currentPlayer) {
            return true;
        }
    }

    // Check columns
    for (int j = 0; j < 3; j++) {
        if (board[0][j] == currentPlayer && board[1][j] == currentPlayer && board[2][j] == currentPlayer) {
            return true;
        }
    }

    // Check diagonals
    if ((board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) ||
        (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer)) {
        return true;
    }

    return false;
}

bool checkDraw() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                return false; // Empty space found, game is not a draw
            }
        }
    }
    return true; // All spaces filled, it's a draw
}

int main() {
    char playAgain = 'y';

    while (playAgain == 'y' || playAgain == 'Y') {
        // Initialize the board
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
        currentPlayer = 'X';

        cout << "Welcome to Tic-Tac-Toe!" << endl;

        while (true) {
            displayBoard();

            int row, col;
            cout << "Player " << currentPlayer << ", enter your move (row and column, 1-3): ";
            cin >> row >> col;

            row--; // Adjust for 0-based indexing
            col--;

            if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
                cout << "Invalid move. Try again." << endl;
                continue;
            }

            board[row][col] = currentPlayer;

            if (checkWin()) {
                displayBoard();
                cout << "Player " << currentPlayer << " wins!" << endl;
                break;
            }

            if (checkDraw()) {
                displayBoard();
                cout << "It's a draw!" << endl;
                break;
            }

            currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        }

        cout << "Play again? (y/n): ";
        cin >> playAgain;
    }

    return 0;
}

# Task 4 :
#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Task {
    string description;
    bool isCompleted;
};

vector<Task> tasks;

void addTask() {
    string description;
    cout << "Enter task description: ";
    getline(cin, description);

    Task newTask;
    newTask.description = description;
    newTask.isCompleted = false;

    tasks.push_back(newTask);
    cout << "Task added successfully!" << endl;
}

void viewTasks() {
    cout << "To-Do List:" << endl;
    for (int i = 0; i < tasks.size(); i++) {
        cout << i + 1 << ". " << tasks[i].description;
        if (tasks[i].isCompleted) {
            cout << " (Completed)" << endl;
        } else {
            cout << " (Pending)" << endl;
        }
    }
}

void markTaskCompleted() {
    int taskNumber;
    cout << "Enter the task number to mark as completed: ";
    cin >> taskNumber;

    if (taskNumber >= 1 && taskNumber <= tasks.size()) {
        tasks[taskNumber - 1].isCompleted = true;
        cout << "Task marked as completed." << endl;
    } else {
        cout << "Invalid task number." << endl;
    }
}

void removeTask() {
    int taskNumber;
    cout << "Enter the task number to remove: ";
    cin >> taskNumber;

    if (taskNumber >= 1 && taskNumber <= tasks.size()) {
        tasks.erase(tasks.begin() + taskNumber - 1);
        cout << "Task removed successfully." << endl;
    } else {
        cout << "Invalid task number." << endl;
    }
}

int main() {
    int choice;

    do {
        cout << "\nTo-Do List Manager" << endl;
        cout << "1. Add Task" << endl;
        cout << "2. View Tasks" << endl;
        cout << "3. Mark Task as Completed" << endl;
        cout << "4. Remove Task" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore(); // Clear newline character from input buffer

        switch (choice) {
            case 1:
                addTask();
                break;
            case 2:
                viewTasks();
                break;
            case 3:
                markTaskCompleted();
                break;
            case 4:
                removeTask();
                break;
            case 5:
                cout << "Exiting..." << endl;
                break;
            default:
                cout << "Invalid choice." << endl;
        }
    } while (choice != 5);

    return 0;
}

# Task 5 :
#include <iostream>
#include <opencv2/opencv.hpp>

using namespace cv;
using namespace std;

int main() {
    Mat image;

    // Load Image
    cout << "Enter the image path: ";
    string imagePath;
    getline(cin, imagePath);
    image = imread(imagePath);

    if (image.empty()) {
        cout << "Could not load the image." << endl;
        return -1;
    }

    // Display Image
    imshow("Original Image", image);
    waitKey(0);

    // Image Processing Options
    int choice;
    do {
        cout << "\nImage Processing Options:" << endl;
        cout << "1. Grayscale" << endl;
        cout << "2. Blur" << endl;
        cout << "3. Sharpen" << endl;
        cout << "4. Adjust Brightness/Contrast" << endl;
        cout << "5. Crop" << endl;
        cout << "6. Resize" << endl;
        cout << "7. Save Image" << endl;
        cout << "8. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: { // Grayscale
                cvtColor(image, image, COLOR_BGR2GRAY);
                imshow("Grayscale Image", image);
                waitKey(0);
                break;
            }
            case 2: { // Blur
                blur(image, image, Size(5, 5)); // Adjust kernel size as needed
                imshow("Blurred Image", image);
                waitKey(0);
                break;
            }
            case 3: { // Sharpen
                Mat kernel = (Mat_<float>(3, 3) <<
                    -1, -1, -1,
                    -1, 9, -1,
                    -1, -1, -1
                );
                filter2D(image, image, -1, kernel);
                imshow("Sharpened Image", image);
                waitKey(0);
                break;
            }
            case 4: { // Adjust Brightness/Contrast
                double alpha = 1.0; // Contrast control (1.0 = no change)
                int beta = 0;       // Brightness control (0 = no change)

                cout << "Enter alpha (contrast): ";
                cin >> alpha;
                cout << "Enter beta (brightness): ";
                cin >> beta;

                image.convertTo(image, -1, alpha, beta);
                imshow("Adjusted Image", image);
                waitKey(0);
                break;
            }
            case 5: { // Crop
                int x, y, width, height;
                cout << "Enter x, y, width, and height for cropping: ";
                cin >> x >> y >> width >> height;

                Rect roi(x, y, width, height);
                Mat croppedImage = image(roi);
                imshow("Cropped Image", croppedImage);
                waitKey(0);
                break;
            }
            case 6: { // Resize
                int newWidth, newHeight;
                cout << "Enter new width and height: ";
                cin >> newWidth >> newHeight;

                resize(image, image, Size(newWidth, newHeight));
                imshow("Resized Image", image);
                waitKey(0);
                break;
            }
            case 7: { // Save Image
                cout << "Enter the output image path: ";
                string outputPath;
                getline(cin, outputPath);
                imwrite(outputPath, image);
                cout << "Image saved successfully!" << endl;
                break;
            }
            case 8:
                cout << "Exiting..." << endl;
                break;
            default:
                cout << "Invalid choice." << endl;
        }
    } while (choice != 8);

    return 0;
}


