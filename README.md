#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSArray *dataArray = @[
            @"111-222",
            @"111-2223",
            @"123-456",
            @"123-789"
        ];

        NSString *pattern = @"111-22*"; // '111-22*' represents the pattern you want

        // Construct the predicate format with 'LIKE' operator and add a wildcard '*'
        NSString *predicateFormat = [NSString stringWithFormat:@"self LIKE[cd] '%@'", [pattern stringByReplacingOccurrencesOfString:@"*" withString:@"%"]];

        // Use NSPredicate to filter array based on the pattern
        NSPredicate *predicate = [NSPredicate predicateWithFormat:predicateFormat];
        NSArray *filteredArray = [dataArray filteredArrayUsingPredicate:predicate];

        // Print the result
        NSLog(@"Result: %@", filteredArray);
    }
    return 0;
}


#import <Foundation/Foundation.h>

void listFilesInDirectory(NSString *directoryPath, NSInteger maxDepth) {
    NSFileManager *fileManager = [NSFileManager defaultManager];

    // Check if the path is a directory
    BOOL isDirectory;
    BOOL exists = [fileManager fileExistsAtPath:directoryPath isDirectory:&isDirectory];

    if (exists && isDirectory) {
        // Call the recursive method to list files
        listFilesInDirectoryRecursive(directoryPath, 0, maxDepth);
    } else {
        NSLog(@"Invalid directory path or not a directory.");
    }
}

void listFilesInDirectoryRecursive(NSString *directoryPath, NSInteger currentDepth, NSInteger maxDepth) {
    NSFileManager *fileManager = [NSFileManager defaultManager];

    NSError *error;
    NSArray *contents = [fileManager contentsOfDirectoryAtPath:directoryPath error:&error];

    if (!error) {
        // Print files in the current directory
        for (NSString *file in contents) {
            NSLog(@"File: %@", file);
        }

        // Check if currentDepth is less than maxDepth
        if (currentDepth < maxDepth) {
            // Recursively call the method for each subdirectory
            for (NSString *subDirectory in contents) {
                NSString *subDirectoryPath = [directoryPath stringByAppendingPathComponent:subDirectory];
                listFilesInDirectoryRecursive(subDirectoryPath, currentDepth + 1, maxDepth);
            }
        }
    } else {
        NSLog(@"Error reading directory: %@", error.localizedDescription);
    }
}

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // Specify the path to the main directory
        NSString *mainDirectoryPath = @"/path/to/your/directory";

        // Set the maximum depth for recursive checking
        NSInteger maxDepth = 2;

        // Call the method to list files in the directory
        listFilesInDirectory(mainDirectoryPath, maxDepth);
    }
    return 0;
}
The objective of the Onboarding Documentation is to provide new members with the necessary information and guidance to quickly familiarize themselves with the work environment, tools, and daily workflows. This comprehensive document aims to ensure a smooth onboarding process and facilitate efficient integration into the team.
Content:
The Onboarding Documentation includes the following sections:
		Environment Setup:
Detailed steps and instructions on how to install the program environment.
Required software, libraries, and dependencies, including download and installation addresses, as well as version requirements.
		Tool Usage:
List of commonly used tools and software, including development environments, code editors, debugging tools, etc.
		Daily Workflows:
Detailed explanation of the team's daily workflows, including version control, branch management, and code submission guidelines.
		Examples and Case Studies:
Provide relevant examples and case studies to demonstrate the practical application of daily workflows.
Examples can include the complete process from task assignment to code submission, helping new members understand how the project operates.
Result:
By creating comprehensive Onboarding Documentation, the company can provide new members with the necessary information and guidance to quickly adapt to the work environment. New members will be able to smoothly set up the environment, use the tools effectively, and understand and adhere to the team's workflows and branch naming conventions. This will increase the efficiency of new members, reduce communication costs, and contribute to the seamless progress of the project.


Project Overview: Macro and Micro Introduction
Objective:
The objective is to provide members with a comprehensive understanding of the project structure and specific functionalities, facilitating their comprehension of the overall project and its specific features. This will be achieved through the creation of a video, PowerPoint presentation (PPT), and directory document, which will offer both macro and micro perspectives on the project's structure and functionalities.
Macro Project Structure:
Create a video that provides an overview of the entire project, including its main objectives, target audience, and how it relates to other tools.
Present a visual representation of the project's overall workflow, helping members grasp its operational dynamics as a whole.
Explain the involvement of other teams in the project and the tools they use. For example, Team A utilizes Tools A and B.
Micro Project:
Develop a directory document containing links to various project functionalities.
Encourage each member to share their understanding of specific functionalities and their corresponding workflows in the document whenever they complete a new feature.
Ensure the document's ownership is transferred to the supervisor to prevent loss of document permissions in case of employee departure.
Result:
By implementing these improvements, the team will be able to provide both macro and micro introductions to the project, enabling members to better comprehend the overall structure and specific functionalities. The creation of videos and directory documents will allow members to quickly grasp the project's workflow and specific features, ultimately enhancing their work efficiency, reducing dependence on others, minimizing errors and defects caused by a lack of project understanding, and fostering collaboration within the team for the smooth progress of the project.




Code Standards and Project Maintenance
Objective: The objective is to enhance the maintainability of the project by implementing a series of measures, including directory structure, code reuse, refactoring, single responsibility, code review, and logging standards, to improve code standards and maintainability.
Action Steps:
		Directory Structure:
Control the depth of directories to avoid excessive levels, making it easier to locate and modify code.
Ensure a clear and easily understandable directory structure to avoid confusion and ambiguity.
		Code Reuse:
Extract common code sections to prevent duplicating and copying the same code in different directories, reducing maintenance difficulties and code complexity. 
UIAlertController instances within each controller
setupLTE
		Refactoring:
Regularly perform code refactoring to remove redundancy and duplicate code, making the system more clear and easier to maintain.
Use refactoring techniques to optimize the code structure, eliminate code bloat, and improve maintainability.
		Single Responsibility:
Each class should be responsible for a single functionality, and each function should handle only one task, 
avoiding multiple classes performing the same tasks or one class handling multiple tasks. 
For instance, the Log class, Timestamp class, and File creation and inspection are currently mixed together, but they should be separated.
Remove duplicate classes, such as eliminating redundant classes like "device" and "deviceP," ensuring that each class has a single responsibility.
		Variable and Code Review:
Conduct code reviews with other team members when adding new variables to avoid overly bloated code.
Regularly perform code reviews among team members to identify potential issues, improve code quality, reduce errors and defects, and enhance code maintainability.
		Logging Output Standards:
Follow standardized logging output practices to ensure clear, readable logs that facilitate problem identification and troubleshooting.
Consider using appropriate log levels and formats, as well as adding necessary contextual information.
Result: By implementing these improvements, code standards and maintainability will be enhanced. Controlling the directory structure, implementing code reuse, and conducting regular code refactoring will make the code clearer, reduce redundancy, and improve maintainability. Adhering to the single responsibility principle will prevent confusion and code duplication. Code reviews and logging output standards will help identify potential issues, improve code quality, enhance code readability, and expedite problem diagnosis. These improvements will lead to reduced errors and defects, improved team collaboration, and the smooth progression of the project.

Testing Functionality and Peer Code Review Process
Situation: The company aims to enhance quality control and team collaboration by improving testing functionality and the peer code review process.
Task: Introduce comprehensive testing functionality and improve the peer code review process to enhance code quality and merge tracking.
Action Steps:
		Introducing Comprehensive Testing Functionality:
Create comprehensive feature to run after bug fixes and new features, ensuring they can be executed with a single click. These tests allow team members to run tests overnight, with the entire test process automatically recorded.
Save test results in different directories and generate test result reports for easy access to view failed test cases.
		Improving Peer Code Review Process:
Enforce peer code reviews for all team members, ensuring that every merge request undergoes careful examination and review.
Introduce a sign-off mechanism, requiring reviewers to sign off on merge requests, indicating that they have thoroughly reviewed and approved the code quality.
Each team member should be responsible for closing merge requests associated with their assigned tickets, ensuring they are eventually merged into the main branch.
Track the status and progress of each merge request, ensuring that they are not left open for an extended period and promptly address any pending items.
Result: These improvements will enhance quality control and team collaboration within the company.
The introduction of comprehensive testing functionality, including comprehensive test cases, automated test runs, and test result reports, will facilitate the quick identification of errors and failure cases.
Improving the peer code review process through mandatory reviews and sign-off mechanisms will ensure that code undergoes careful scrutiny, leading to improved code quality.
Each team member taking responsibility for closing their assigned merge requests will ensure timely processing and merging into the main branch.
By tracking the status and progress of merge requests and leveraging test result reports, better visibility into test failure cases and project status can be achieved, enhancing project management efficiency.
These improvement measures will increase team members' focus on quality control and collaboration, reduce errors and defects, and foster effective teamwork and project success. Additionally, the use of test result reports and merge tracking will provide better insight into test failures and project progress, improving project visibility and management efficiency.
