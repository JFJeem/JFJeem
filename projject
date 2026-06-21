//Student portal management
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Student
{
    int id;
    char name[100];
    char department[50];
    char phone[20];
    float cgpa;
};

struct Student s;

int login();
void addStudent();
void displayStudents();
void searchStudent();
void updateStudent();
void deleteStudent();
void countStudents();
int checkID(int);

int main()
{
    int choice;

    if(!login())
    {
        printf("\nAccess Denied!\n");
        return 0;
    }

    while(1)
    {
        printf("   STUDENT MANAGEMENT SYSTEM\n");
        printf("=====================================\n");
        printf("1. Add Student\n");
        printf("2. Display Students\n");
        printf("3. Search Student\n");
        printf("4. Update Student\n");
        printf("5. Delete Student\n");
        printf("6. Count Students\n");
        printf("7. Exit\n");
        printf("=====================================\n");

        printf("Enter Choice: ");
        scanf("%d",&choice);

        switch(choice)
        {
        case 1:
            addStudent();
            break;

        case 2:
            displayStudents();
            break;

        case 3:
            searchStudent();
            break;

        case 4:
            updateStudent();
            break;

        case 5:
            deleteStudent();
            break;

        case 6:
            countStudents();
            break;

        case 7:
            printf("\nThank You!\n");
            exit(0);

        default:
            printf("\nInvalid Choice!\n");
        }
    }

    return 0;
}

int login()
{
    char username[30];
    char password[30];

    printf("========== ADMIN LOGIN ==========\n");

    printf("Username: ");
    scanf("%s",username);

    printf("Password: ");
    scanf("%s",password);

    if(strcmp(username,"CSE1290")==0 &&
       strcmp(password,"123456")==0)
    {
        printf("\nLogin Successful!\n");
        return 1;
    }

    return 0;
}

int checkID(int id)
{
    FILE *fp;

    fp = fopen("student.dat","rb");

    if(fp == NULL)
        return 0;

    while(fread(&s,sizeof(s),1,fp))
    {
        if(s.id == id)
        {
            fclose(fp);
            return 1;
        }
    }

    fclose(fp);
    return 0;
}

void addStudent()
{
    FILE *fp;

    fp = fopen("student.dat","ab");

    if(fp == NULL)
    {
        printf("File Error!\n");
        return;
    }

    printf("\nEnter Student ID: ");
    scanf("%d",&s.id);

    if(checkID(s.id))
    {
        printf("ID Already Exists!\n");
        fclose(fp);
        return;
    }

    getchar();

    printf("Enter Name: ");
    fgets(s.name,sizeof(s.name),stdin);
    s.name[strcspn(s.name,"\n")] = 0;

    printf("Enter Department: ");
    fgets(s.department,sizeof(s.department),stdin);
    s.department[strcspn(s.department,"\n")] = 0;

    printf("Enter Phone: ");
    fgets(s.phone,sizeof(s.phone),stdin);
    s.phone[strcspn(s.phone,"\n")] = 0;

    printf("Enter CGPA: ");
    scanf("%f",&s.cgpa);

    fwrite(&s,sizeof(s),1,fp);

    fclose(fp);

    printf("\nStudent Added Successfully.\n");
}

void displayStudents()
{
    FILE *fp;

    fp = fopen("student.dat","rb");

    if(fp == NULL)
    {
        printf("\nNo Records Found!\n");
        return;
    }

    printf("\n=====================================================================\n");
    printf("ID\tName\t\tDepartment\tPhone\t\tCGPA\n");
    printf("=====================================================================\n");

    while(fread(&s,sizeof(s),1,fp))
    {
        printf("%d\t%s\t%s\t%s\t%.2f\n",
               s.id,
               s.name,
               s.department,
               s.phone,
               s.cgpa);
    }

    fclose(fp);
}

void searchStudent()
{
    FILE *fp;
    int id, found = 0;

    fp = fopen("student.dat","rb");

    if(fp == NULL)
    {
        printf("No Records Found!\n");
        return;
    }

    printf("Enter ID to Search: ");
    scanf("%d",&id);

    while(fread(&s,sizeof(s),1,fp))
    {
        if(s.id == id)
        {
            printf("\nStudent Found\n");
            printf("ID         : %d\n",s.id);
            printf("Name       : %s\n",s.name);
            printf("Department : %s\n",s.department);
            printf("Phone      : %s\n",s.phone);
            printf("CGPA       : %.2f\n",s.cgpa);

            found = 1;
            break;
        }
    }

    if(!found)
        printf("Student Not Found!\n");

    fclose(fp);
}

void updateStudent()
{
    FILE *fp;
    int id, found = 0;

    fp = fopen("student.dat","rb+");

    if(fp == NULL)
    {
        printf("No Records Found!\n");
        return;
    }

    printf("Enter ID to Update: ");
    scanf("%d",&id);

    while(fread(&s,sizeof(s),1,fp))
    {
        if(s.id == id)
        {
            found = 1;

            getchar();

            printf("Enter New Name: ");
            fgets(s.name,sizeof(s.name),stdin);
            s.name[strcspn(s.name,"\n")] = 0;

            printf("Enter New Department: ");
            fgets(s.department,sizeof(s.department),stdin);
            s.department[strcspn(s.department,"\n")] = 0;

            printf("Enter New Phone: ");
            fgets(s.phone,sizeof(s.phone),stdin);
            s.phone[strcspn(s.phone,"\n")] = 0;

            printf("Enter New CGPA: ");
            scanf("%f",&s.cgpa);

            fseek(fp,-sizeof(s),SEEK_CUR);
            fwrite(&s,sizeof(s),1,fp);

            printf("\nRecord Updated Successfully.\n");
            break;
        }
    }

    if(!found)
        printf("Student Not Found!\n");

    fclose(fp);
}

void deleteStudent()
{
    FILE *fp,*temp;
    int id, found = 0;

    fp = fopen("student.dat","rb");
    temp = fopen("temp.dat","wb");

    if(fp == NULL)
    {
        printf("No Records Found!\n");
        return;
    }

    printf("Enter ID to Delete: ");
    scanf("%d",&id);

    while(fread(&s,sizeof(s),1,fp))
    {
        if(s.id == id)
        {
            found = 1;
        }
        else
        {
            fwrite(&s,sizeof(s),1,temp);
        }
    }

    fclose(fp);
    fclose(temp);

    remove("student.dat");
    rename("temp.dat","student.dat");

    if(found)
        printf("Record Deleted Successfully.\n");
    else
        printf("Student Not Found!\n");
}

void countStudents()
{
    FILE *fp;
    int count = 0;

    fp = fopen("student.dat","rb");

    if(fp == NULL)
    {
        printf("No Records Found!\n");
        return;
    }

    while(fread(&s,sizeof(s),1,fp))
    {
        count++;
    }

    fclose(fp);

    printf("\nTotal Students = %d\n",count);
}

