# CGPA-calculator
#include<iostream>
#include<vector>
using namespace std;

class Subject{
    public:
    string subjectname;
    int credit;
    float gradepoint;

    //constructor
    Subject(string num,int cr,float gp)
    {
        subjectname = num;
        credit = cr;
        gradepoint = gp;
    }

};

class Student{
    public:
    string name;
    vector<Subject>subjects;

    //constructor
    Student(string studentName)
    {
        name = studentName;
    }
    void addSubject(string subjectName, int credit, float gradepoint)
    {
        Subject newSubject(subjectName, credit, gradepoint);
        subjects.push_back(newSubject);
    }

    float calculatecgpa()
    {
        int totalcredit = 0;
        float weightgradepoint = 0;
        for(const Subject & subject : subjects)
        {
            totalcredit += subject.credit;
            weightgradepoint += subject.credit * subject.gradepoint;
        }
        return(totalcredit>0) ? (weightgradepoint / totalcredit): 0;
    }

    void displaycgpa()
    {
        cout<<"Student name : "<< name <<endl;
        float cgpa = calculatecgpa();
        cout<< "CGPA : "<< cgpa <<endl;
    }
   // void addSubject(string subjectname, int credit, float gradepoint);
};

int main(){
    string studentname;
    int numsub;

    cout<<"enter student's name : ";
    getline(cin, studentname);

    cout<<"enter the number of subjects : ";
    cin>>numsub;

    Student student(studentname);

    cin.ignore();// flush newline after numsub

    for(int i=0; i < numsub; i++){
        string subjectname;
        int credit;
        float gradepoint;

        cout<<"enter the subject's name : ";
        getline(cin, subjectname);

        cout<<"enter the credit : ";
        cin>>credit;

        cout<<"enter the gradepoint : ";
        cin>>gradepoint;

        cin.ignore();// to handle next getline properly
        
        //Add the subject to the student's record
        student.addSubject(subjectname, credit, gradepoint);
    }
    //Calculate and display the CGPA
    student.displaycgpa();
    return 0;
}
