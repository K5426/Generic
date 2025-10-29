#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int compare(const void* left,const void* right){
	float *k=(float*)left;
	float *g=(float*)right;
	if(*k<*g){return -1;}
	if(*k>*g){return 1;}
	if(*k==*g){return 0;}
}
void insertion(void *arr,size_t ele_size,size_t arr_size,int (*comp)(const void*,const void*)){
	char *temp=(char*)malloc(ele_size);
	char *Arr=(char*)arr;
	for(size_t i=1;i<arr_size;i++){
		memcpy(temp,Arr+(ele_size*i),ele_size);
		int j=i-1;
		while(j>=0 && comp(Arr+(ele_size*j),temp)>0){
			memcpy(Arr+(ele_size*(j+1)),Arr+(ele_size*j),ele_size);
			j-=1;
		}
		memcpy(Arr+(ele_size*(j+1)),temp,ele_size);
	}
	free(temp);
}
int main(){
	float a[10]={8.79,4.56,11.0,2.89,55.9,6.0098,7.891,1.002,9.101,12};
	insertion(a,sizeof(float),10,compare);
	for(int i=0;i<10;i++){
		printf("%f ",a[i]);
	}
}
