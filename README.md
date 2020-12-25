# Contact-manangement-System
#include <stdio.h>
#include <conio.h>
#include <string.h>
#include <stdlib.h>
#include <windows.h>

int dmenu();//main menu
void dinsert();//to add contact
void dmodify();//to modify or edit a contact
void dsearch();//to search for a contact
void dview();// to view all contacts
void ddelete();//to delete a contact

struct dnode{
    char dlname[20], dfname[20], dtel[15], demail[20],daddress[20];
    struct dnode *dnext;
};
typedef struct dnode node;
node *dstart, *dtemp;
int dmenu()
{
    int dch;

        printf("CONTACT MANAGEMENT SYSTEM\n");
        printf("==================================\n");
       printf("------WELCOME------\n");
        printf("1: Add new contact.\n");
        printf("2:Modify contact.\n");
        printf("3:Search Contact.\n");
         printf("4:View all contacts.\n");
        printf("5:Delete contact.\n");
         printf("6:EXIT\n");
         printf("SELECT FROM (1-6)\n");

         scanf("%d", &dch);
        return dch;
}


void dinsert()
{
    node *dptr,*dprev;
    dtemp=(node *)malloc(sizeof(node));
    printf("First name: ");
    scanf("%s",dtemp->dfname);
    printf("Last name: ");
    scanf("%s",dtemp->dlname);
    printf("Phone number: ");
    scanf("%s",dtemp->dtel);
    printf("Email Address: ");
    scanf("%s",dtemp->demail);
    printf("Home Address: ");
    scanf("%s",dtemp->daddress);
    dtemp->dnext=NULL;
    if (dstart==NULL)
        dstart=dtemp;
    else{
        dprev=dptr=dstart;
    }
        while (strcmp(dtemp->dfname,dptr->dfname)>0){
            dprev=dptr;
            dptr=dptr->dnext;
            if(dptr==NULL) break;
        }
        if(dptr==dprev){
            dtemp->dnext=dstart;
            dstart=dtemp;
        }
        else if(dptr==NULL)
            dprev->dnext=dtemp;
        else{
            dtemp->dnext=dptr;
            dprev->dnext=dtemp;
        }
    }
void dmodify()
{
        node *dptr;
    char dstr[20];
    if(dstart==NULL){
        printf("\n\t\t\t CONTACT MANAGEMENT SYSTEM is Empty........\n");
        getch();
        return;
    }
    printf("First name to edit : ");
    scanf("%s", dstr);
    dptr=dstart;
    while(strcmp(dptr->dfname,dstr)!=0)
    {
        dptr= dptr->dnext;
        if (dptr==NULL) break;
    }
    if(dptr!=NULL){
        printf("First Name : %s" ,dptr->dfname);
        scanf("%s",dptr->dfname);
        printf("Last Name: %s", dptr->dlname);
        scanf("%s",dptr->dlname);
         printf("Phone Number: %s", dptr->dtel);
         scanf("%s",dptr->dtel);
         }
     else{
        printf("No Matching Records......\n");
        getch();
     }
}
void dsearch()
{
        node *dptr;
    char dstr[20];
    if(dstart==NULL){
        printf("\n\t\t\tContact Management System is Empty...\n");
        getch();
        return;
          }
          printf("Last Name: %s" ,dptr->dlname);
          scanf("%s",dptr->dlname);
        printf("Name to Search: ");
        scanf("%s",dstr);
    dptr=dstart;
    while(strcmp(dptr->dfname,dstr)!=0){
        dptr=dptr->dnext;
        if(dptr==NULL) break;
    }
    if(dptr!=NULL){
        printf("First name: %s\n",dptr->dfname);
        printf("Last name: %s\n",dptr->dlname);
        printf("Phone number: %s\n",dptr->dtel);
        printf("Email: %s\n",dptr->demail);
        printf("Home Address: %s\n",dptr->daddress);
    }
    else{
        printf("No Matching Records...");
    }
     getch();
}
void dview()
{
    node *dptr;
    if(dstart==NULL){
        printf("Contact Management System is Empty...\n");
        getch();
        return;
    }

    printf("\t\t----------------------------\n");
    for(dptr=dstart; dptr!=NULL; dptr=dptr->dnext){
        printf("\t\tFirst name: %s",dptr->dfname);
        printf("\t\tLast name: %s",dptr->dlname);
        printf("\t\tPhone number: %sn",dptr->dtel);
        printf("\t\tEmail: %s",dptr->demail);
        printf("\t\tHome Address: %s",dptr->daddress);
        printf("\n\t\t----------------------------\n");
    }
    getch();
}
void ddelete()
{
     node *dptr,*dprev,*dtemp;
    char dstr[20],dyn='n';
    if(dstart==NULL){
         printf("Contact Management System is Empty...\n");
        getch();
        return;
    }
    printf("First name to delete: ");
    scanf("%s",dstr);
    dprev=dptr=dstart;
    while(strcmp(dptr->dfname,dstr)!=0){
        dprev=dptr;
        dptr=dptr->dnext;
        if(dptr==NULL) break;
    }
    if(dptr!=NULL){
        printf("\nDeleting Record......Confirm[y/n] ");
        dyn=getch();
        printf("\n\n-------------------------------------------------");
        printf("\t\tFirst name: %s",dptr->dfname);
        printf("\t\tLast name: %s",dptr->dlname);
        printf("\t\tPhone number: %sn",dptr->dtel);
        printf("\t\tEmail: %s",dptr->demail);
        printf("\t\tHome Address: %s",dptr->daddress);
        printf("-------------------------------------------------");
            if(dyn=='y'){
                if(dptr==dstart){
                    dtemp=dstart->dnext;
                    free(dstart);
                    dstart=dtemp;
                }
                else{
                    dtemp=dptr->dnext;
                    free(dptr);
                    dprev->dnext=dtemp;
                }
               }

             else{
            printf("\nRecord not deleted...");
        }
        }else{
              printf("No Matching Record....");
        }
    getch();

}
void  main()
{
    int dch;
    dstart=(node *)malloc(sizeof(node));
    dstart=NULL;
    do{

        dch=dmenu();
           switch(dch){
            case 1: dinsert();
            break;
            case 2: dmodify();
            break;
            case 3: dsearch();
            break;
            case 4: dview();
            break;
            case 5: ddelete();
            break;
        }
    }
    while(dch!=6);

}
 
