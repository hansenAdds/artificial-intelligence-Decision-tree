
#include <fstream>
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>
#include <stdlib.h>
#include <math.h>
using namespace std;


int array[2];
vector<float> lab;
bool flagg;
vector<string> output;
vector<string> flabel;
struct Node{
    float att_index;
    Node* left;
    Node* right;
    string label;
    float splitval;
    bool leaf;
};


float lg2(float n)
{
   return log(n)/log(2)*1.0;
}
Node* newnode(float index,float split,string labell,bool isleaf){   	//create a new node
	Node* node=new Node();
	node->att_index=index;
	node->label=labell;
	node->left=NULL;
	node->right=NULL;
	node->splitval=split;
    node->leaf=isleaf;
	return node;
}
vector<vector<float> > gettable(string filename){
    int count=0;
    int record=0;
    string line;
    string temp;
    vector<string> out;

    vector<string> data;
    vector<vector<string> > haha;
    ifstream input(filename);

       if (input.is_open()) {
        while (getline(input, line)) {
             count++;
             if (count==1) continue;

                for(int i=0;i<line.length();i++){

                    if (line[i]!=32){
                        temp+=line[i];
                        if(line[i+1]==32||i==(line.length()-1)){
                            data.push_back(temp);
                            temp.erase();
                        }
                    }
                }
                haha.push_back(data);
                data.clear();

        }
        input.close();

       }

    vector<vector<float> > newdata;
    vector<float> tempp;


    for(int i=0;i<haha.size();i++){
        output.push_back(haha[i].back());   //out value
    }
    for(int i=0;i<haha.size();i++){
        haha[i].back()=to_string(i);
    }

    for(int i=0;i<haha.size();i++){
          for(int k=0;k<haha[0].size();k++){
             tempp.push_back(stof(haha[i][k]));
          }
        newdata.push_back(tempp);
        tempp.clear();
    }



      return newdata;

}
vector<vector<float> > gettest(string filename){
        int count=0;

        string temp;
        string line;

    vector<string> data;

        vector<vector<string> > haha;

    ifstream input(filename);

       if (input.is_open()) {
        while (getline(input, line)) {
             count++;
             if (count==1) continue;

                for(int i=0;i<line.length();i++){

                    if (line[i]!=32){
                        temp+=line[i];
                        if(line[i+1]==32||i==(line.length()-1)){
                            data.push_back(temp);
                            temp.erase();
                        }
                    }
                }
                haha.push_back(data);
                data.clear();

        }
        input.close();

       }
   vector<vector<float> > newdata;
    vector<float> tempp;


    for(int i=0;i<haha.size();i++){
          for(int k=0;k<haha[0].size();k++){
             tempp.push_back(stof(haha[i][k]));
          }
        newdata.push_back(tempp);
        tempp.clear();
    }



      return newdata;

}


float info(vector<vector<float> > data){  //get the information content
    float aaa=0;
    float aa=0;
    float a=0;
    float bbb=0;
    float bb=0;
    float b=0;
    float ccc=0;
    float sum=data.size();
    float infoval=0;
    float temp=0;
        float temp1=0;
    float temp2=0;
    float temp3=0;
    float temp4=0;
    float temp5=0;
    float temp6=0;
   ;

    for(int i=0;i<data.size();i++){    //the train data output labels
        if (output[data[i].back()]=="AAA"){
            aaa++;
        }
        else if (output[data[i].back()]=="AA"){
            aa++;
        }
        else if (output[data[i].back()]=="A"){
            a++;
        }
        else if (output[data[i].back()]=="BBB"){
            bbb++;
        }
        else if (output[data[i].back()]=="BB"){
            bb++;
        }
        else if (output[data[i].back()]=="B"){
            b++;
        }
        else if (output[data[i].back()]=="CCC"){
            ccc++;
        }
    }
    if (aaa>0){  //avoid the zero case
        temp=-(aaa/sum)*lg2(aaa/sum);
    }
    if (aa>0){
        temp1=-(aa/sum)*lg2(aa/sum);
    }
    if (a>0){
        temp2=-(a/sum)*lg2(a/sum);
    }
    if (bbb>0){
        temp3=-(bbb/sum)*lg2(bbb/sum);
    }
     if (bb>0){
        temp4=-(bb/sum)*lg2(bb/sum);
    }
     if (b>0){
        temp5=-(b/sum)*lg2(b/sum);
    }
    if (ccc>0){
        temp6=-(ccc/sum)*lg2(ccc/sum);
    }

    return float(temp+temp1+temp2+temp3+temp4+temp5+temp6);



}
vector<vector<float>>  cut(int attr,vector<vector<float>> tdata,float splitval,bool nb ){   //cut the data to left and rightside
    vector<vector<float>> left;
    vector<vector<float>> right;

    for(int i=0;i<tdata.size();i++){
        if (tdata[i][attr]<=splitval){
            left.push_back(tdata[i]);
        }
        else{
            right.push_back(tdata[i]);
        }
    }
  
    if (nb==true){   
        return left;
    }   
    else{
        return right;
    }
   
}

vector<float> choose_split(vector<vector<float> > data){
    float best=-99;
    float bestsplit=0;
    float bestattr=0;
float sp;
    vector<vector<float> > record=data;
  

   
    float sizee=data.size();
    for(int i=0;i<5;i++){

        // cout<<iroot<<" "<<endl;
        for(int g=0;g<data.size();g++){
            data[g].back()=record[g].back();

        }
       

        for(int k=0;k<data.size();k++){                //sort
            for(int j=0;j<data.size()-k-1;j++){
                if (data[j][i]>data[j+1][i]){

                    float temp=data[j+1][i];
                    float last=data[j+1].back();

                    data[j+1][i]=data[j][i];
                    data[j+1].back()=data[j].back();

                    data[j][i]=temp;
                    data[j].back()=last;
                }
            }
        }


        for(int u=0;u<data.size()-2;u++){
       

           sp=float((data[u][i]+data[u+1][i])*0.5);
        
       

            vector<vector<float>> leftt=cut(i,data,sp,true);
         
      
             vector<vector<float>> rightt=cut(i,data,sp,false);

        


            float reminder=float(info(leftt)*(leftt.size()*1.0/sizee))  +  float(info(rightt)*(rightt.size()*1.0/sizee));

           
           float iroot=info(data);


            float gain=iroot-float(reminder);   //info gain
        
            if (gain>best){
                 best=gain;
                 bestsplit=sp;
                 bestattr=i;

            }
        }
     }

    vector<float> back;
    back.clear();
    back.push_back(bestattr);
    back.push_back(bestsplit);
    return back;

}


bool sameinput(vector<vector<float> > data){  //condition for same input 
    bool flag;
    float label=data[0][0];
    for(int i=0;i<data.size();i++){
        for(int k=0;k<data[0].size()-1;k++){
            if (data[i][k]==label){
                flag=true;
            }
            else{
                flag=false;
                break;
            }
        }
    }
    return flag;
}

bool sameoutput(vector<vector<float> > data){  //if statement for same output
    float label=data[0].back();
    bool flag;
    for(int i=0;i<data.size();i++){
        if(data[i].back()==label){
            flag=true;
        }
        else{
            flag=false;
            break;
        }
    }
    return flag;
}


string unique(vector<vector<float> > data){  //condition about unique value
    float count;
    float aa=0;
    float bb=0;
    float aaa=0;
    float bbb=0;
    float a=0;
    float b=0;
    float ccc=0;
    vector<float> record;
    float max=-1;
    string maxx;
    for(int i=0;i<data.size();i++){
        if (output[data[i].back()]=="AAA"){
            aaa++;
            if (aaa>max){
                max=aaa;
                maxx="AAA";
            }
        }
        if (output[data[i].back()]=="AA"){
            aa++;
            if (aa>max){
                max=aa;
                maxx="AA";
            }
        }
        if (output[data[i].back()]=="A"){
            a++;
            if (a>max){
                max=a;
                maxx="A";
            }
        }
        if (output[data[i].back()]=="BBB"){
            bbb++;
            if (bbb>max){
                max=bbb;
                maxx="BBB";
            }
        }
        if (output[data[i].back()]=="BB"){
            bb++;
            if (bb>max){
                max=bb;
                maxx="BB";
            }
        }if (output[data[i].back()]=="B"){
            b++;
            if (b>max){
                max=b;
                maxx="B";
            }
        }
        if (output[data[i].back()]=="CCC"){
            ccc++;
            if (ccc>max){
                max=ccc;
                maxx="CCC";
            }
        }

    }

    return maxx;
    

}
bool isunique(vector<vector<float> > data){  //xx
    float count;
    float aa=0;
    float bb=0;
    float aaa=0;
    float bbb=0;
    float a=0;
    float b=0;
    float ccc=0;
    vector<float> record;
    float max=-1;
    string maxx;
    bool flag;
    for(int i=0;i<data.size();i++){
        if (output[data[i].back()]=="AAA"){
            aaa++;
            if (aaa>max){
                max=aaa;
                maxx="AAA";
            }
        }
        if (output[data[i].back()]=="AA"){
            aa++;
            if (aa>max){
                max=aa;
                maxx="AA";
            }
        }
        if (output[data[i].back()]=="A"){
            a++;
            if (a>max){
                max=a;
                maxx="A";
            }
        }
        if (output[data[i].back()]=="BBB"){
            bbb++;
            if (bbb>max){
                max=bbb;
                maxx="BBB";
            }
        }
        if (output[data[i].back()]=="BB"){
            bb++;
            if (bb>max){
                max=bb;
                maxx="BB";
            }
        }if (output[data[i].back()]=="B"){
            b++;
            if (b>max){
                max=b;
                maxx="B";
            }
        }
        if (output[data[i].back()]=="CCC"){
            ccc++;
            if (ccc>max){
                max=ccc;
                maxx="CCC";
            }
        }

    }
    record.push_back(aaa);
    record.push_back(aa);
    record.push_back(a);
    record.push_back(bbb);
    record.push_back(bb);
    record.push_back(b);
    record.push_back(ccc);

    sort(record.begin(),record.end());

    for(int i=0;i<record.size()-1;i++){
        if (max==record[i]||max==0){
            flag=true;
            break;

        }
        else{
            flag=false;

        }
    }
    return flag;  

}
Node* dtl(vector<vector<float> > data,int minleaf){  //build the tree
    if (data.size()<=minleaf||sameoutput(data)==true||sameinput(data)==true){
        Node* node=newnode(0,0,"",true);
        if (isunique(data)==false){
            // cout<<unique(data)<<" ";
            node->label=unique(data);
        }
        else{
            node->label="unknown";
        }
        return node;
    }

    vector<float> haha=choose_split(data);
    Node* node=newnode(0,0,"",false);
    node->splitval=haha[1];
    // cout<<haha[0]<<" "<<haha[1]<<endl;;
    node->att_index=haha[0];
    node->left=dtl(cut(node->att_index,data,node->splitval,true),minleaf);
    node->right=dtl(cut(node->att_index,data,node->splitval,false),minleaf);
    
    return node;
}
void predict(Node* node,vector<vector<float> > data){   //predict 
    vector<string> record;
  
   for(int i=0;i<data.size();i++){
    const Node* haha=node;
    while (haha->leaf==false){
        if (data[i][haha->att_index]<=haha->splitval){
            haha=haha->left;
            
        }
        else{
            haha=haha->right;

        }


    }     
      flabel.push_back(haha->label);
    
    }
}






int main(int argc,char *argv[]){

    string haha=string(argv[1]);
    string niubi=string(argv[2]);
   

  
   string cao=string(argv[3]);


   vector<vector<float> > input=gettable(haha);


    vector<vector<float> > input2=gettest(niubi);
   


  
    Node* root=dtl(input,stoi(cao));

    predict(root,input2);
    for(int i=0;i<flabel.size();i++){
        cout<<flabel[i]<<endl;
    }

}

// 
