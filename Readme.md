Problem-Hackathon Contract To complete this challenge we need to write a function that will help us find the winning project of the hackathon.
The winning project will be determined by the average score of all of its ratings.   The Hackathon.sol contract is partially setup already. 
Let's discuss the setup in details!   Your Goal: Find Winner Function Create an external, view function findWinner which returns a Project.
In this function, use the projects storage array to find the project that has the highest average rating amongst its array of ratings. 
Upon finding the highest average, return the project.

Solution-

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

contract Hackathon {
    struct Project {
        string title;
        uint[] ratings;
    }
    
    Project[] projects;

    function findWinner() external view returns(Project memory) {
        Project memory topProject; 
        uint topAverage = 0;
        for(uint i = 0; i < projects.length; i++) {
            uint sum;
            for(uint j = 0; j < projects[i].ratings.length; j++) {
                sum += projects[i].ratings[j];
            }
            uint average = sum / projects[i].ratings.length;
            if(average > topAverage) {
                topAverage = average;
                topProject = projects[i];
            }
        }
        return topProject;
    }

    function newProject(string calldata _title) external {
        // creates a new project with a title and an empty ratings array
        projects.push(Project(_title, new uint[](0)));
    }

    function rate(uint _idx, uint _rating) external {
        // rates a project by its index
        projects[_idx].ratings.push(_rating);
    }
}
