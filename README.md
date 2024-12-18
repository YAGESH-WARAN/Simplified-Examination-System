# Simplified-Examination-System
class Staff:
    sid=1000
    slist={}
    f=False
    
class Exam:
   ques=[]
   nq=0

def stafLogin():
    while(True):
        print("1.Create Exam \n2.Approve\n3.Report\n4.Logout\n")
        ch=int(input("Enter choice: "))
        if ch==1:
            if Staff.f:
                print("You have already created the exam")
            else:
                Staff.f=True
                try:
                    n=int(input("Enter No of Questions: "))
                except:
                    print("Enter valid Number...")
                    try:
                        n=int(input("Enter No of Questions: "))
                    except:
                        n=0
                Exam.nq=n
                for i in range(1,n+1):
                    print("Enter Question: ",i)
                    q=input() 
                    op1=input("Option 1: ")
                    op2=input("Option 2: ")
                    op3=input("Option 3: ")
                    ans=input("Answer: ")
                    Exam.ques.append([q,op1,op2,op3,ans])
        elif ch==2:
            for i in Staff.slist:
                if Staff.slist[i][4]=="Pending":
                    if Staff.slist[i][3]>=Exam.nq/2:
                        Staff.slist[i][4]="Pass"
                    else:
                        Staff.slist[i][4]="Fail"
        elif ch==3:
            file=open("Report.txt","w")
            s=""
            for i in Staff.slist:
                file.write("Name \t Roll No \t Mark \t Grade \n")
                s=str(Staff.slist[i][0])+"\t"+str(Staff.slist[i][2])+"\t"+str(Staff.slist[i][3])+"\t"+str(Staff.slist[i][4])
                file.write(s+'\n')
            file.close()
        else:
            break
        
def stdLogin(reg):
    while(True):
        r=0
        print("1. Attend Exam \n2.Show Status \n3.Sign Out\n")
        c=int(input("Enter Your Choice: "))
        if c==1:
            if Staff.f==False:
                print("Exam Not Created Try again....\n")
            else:
                Staff.slist[reg][4]="Pending"
                mark=0
                for i in Exam.ques:
                    print("Question ",(r+1))
                    print("\n",i[0])
                    print("Opt1: ",i[1])
                    print("Opt2: ",i[2])
                    print("Opt3: ",i[3])
                    ans=input("Enter the Answer: ")
                    if ans==i[4]:
                        mark+=1
                    r+=1
                Staff.slist[reg][3]=mark
        elif c==2:
            print("\n-----------------------Student Status----------------------\n")
            print(*Staff.slist[reg],sep=" ")
        else:
            break
 
print("                                        EXAMINATION                ")  
print("---------------------------------------------------------------------------------------\n") 
while(True):
    print("\n1.Staff\n2.Student\n3.Exit\n")
    c=int(input("Enter choice: "))
    if c==1:
        us=input("Enter Staff Name: ")
        ps=input("\nEnter Password: ")
        if us=="ajay" and ps=="123":
            print("Login Successfully....\n\n")
            stafLogin()
        else:
            print("Username or Password Incorrect........Try again!\n")
    elif c==2:
        while(True):
            print("1.Sign Up\n2.Sign In\n3.Logout\n")
            ch=int(input("Enter Your Choice: "))
            if ch==1:
                sname=input("Enter Name: ")
                spass=input("Enter password: ")
                print("Your Register No is : ",Staff.sid)
                Staff.slist[Staff.sid]= [sname,spass,Staff.sid,"0","Not Attended"]
                Staff.sid+=1
                
            elif ch==2:
                reg=int(input("Enter Your Register No: "))
                pss=input("Enter password: ")
                if Staff.slist[reg][1]==pss:
                    print("Login successfully......\n")
                    stdLogin(reg)
                else:
                    print("Incorrect ID/Password......\n")
            else:
                break
    else:
        break
