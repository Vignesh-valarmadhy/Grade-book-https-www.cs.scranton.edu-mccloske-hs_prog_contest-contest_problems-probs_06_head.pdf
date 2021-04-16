# Grade-book-https-www.cs.scranton.edu-mccloske-hs_prog_contest-contest_problems-probs_06_head.pdf

#include <stdio.h>
#include <string.h>

typedef struct
{
    char StudentName[10];
    char grade;
    int Marks[10];
    float gradeNo;
} StudentDetails;

typedef struct
{
    char SubjectName[10];
    int NoStudents;
    int NoWeights;
    float Totalweight;
    float Weights[10];
    StudentDetails Stu[10];
} GradeBook;

int GetnoSubject()
{
    int n;
    scanf("%d", &n);
    return n;
}
StudentDetails GetstudentDetails(int r)
{
    StudentDetails s;
    scanf("%s", s.StudentName);
    for (int g = 0; g < r; g++)
    {
        scanf("%d", &s.Marks[g]);
    }
    return s;
}
GradeBook GetSubjectDetailsOne()
{
    GradeBook G;
    scanf("%9s", G.SubjectName);
    scanf("%d %d", &G.NoStudents, &G.NoWeights);
    G.Totalweight = 0;
    for (int j = 0; j < G.NoWeights; j++)
    {
        scanf("%f", &G.Weights[j]);
        G.Totalweight = G.Totalweight + G.Weights[j];
    }
    for (int k = 0; k < G.NoStudents; k++)
    {
        G.Stu[k] = GetstudentDetails(G.NoWeights);
    }
    return G;
}

GradeBook GetSubjectDetailsN(int n, GradeBook G[n])
{
    for (int i = 0; i < n; i++)
    {
        G[i] = GetSubjectDetailsOne();
    }
}

char getgrade(float s)
{
    char grade;
    if (s < 60)
    {
        grade = 'F';
        return grade;
    }
    else if (s >= 60 && s < 70)
    {
        grade = 'D';
        return grade;
    }
    else if (s >= 70 && s < 80)
    {
        grade = 'C';
        return grade;
    }
    else if (s >= 80 && s < 90)
    {
        grade = 'B';
        return grade;
    }
    else
    {
        grade = 'A';
        return grade;
    }
}

void computeOne(GradeBook *r)
{
    for (int j = 0; j < r->NoStudents; j++)
    {
        float sum = 0;
        for (int i = 0; i < r->NoWeights; i++)
        {
            sum = sum + (r->Weights[i] * r->Stu[j].Marks[i]);
        }
        sum = sum / r->Totalweight;
        r->Stu[j].gradeNo = sum;
        r->Stu[j].grade = getgrade(sum);
    }
}
void computeN(int n, GradeBook a[n])
{
    for (int i = 0; i < n; i++)
    {
        computeOne(&a[i]);
    }
}
void DisplayOne(GradeBook G)
{
    for (int i = 0; i < G.NoStudents; i++)
    {
        printf("%s      %0.2f      %c\n", G.Stu[i].StudentName, G.Stu[i].gradeNo, G.Stu[i].grade);
    }
    printf("\n \n");
}
void DisplayN(int n, GradeBook G[n])
{

    for (int i = 0; i < n; i++)
    {
        printf("%s\n", G[i].SubjectName);
        DisplayOne(G[i]);
    }
}

int main()
{
    int n;
    n = GetnoSubject();
    GradeBook G[n];
    GetSubjectDetailsN(n, G);
    computeN(n, G);
    printf("\n Output:\n \n");
    DisplayN(n, G);
}
