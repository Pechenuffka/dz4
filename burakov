#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void search(int num, int graph[num][num], char names[num]){
    int stepen;
    printf("Enter stepen: ");
    scanf("%d", &stepen);
    
    int degree[num];
    
    for(int i=0 ;i<num; i++){
        degree[i] = 0;
        for(int j=0; j<num; j++){
            degree[i] += graph[i][j];
            degree[i] += graph[j][i];
        }
    }
    
    for(int i=0; i<num; i++){
        if(degree[i] == stepen){
            printf("%c ", names[i]);
        }
    }
}

int main(){
    printf("num: ");
    int n;
    scanf("%d",&n);
    getchar(); // to ignore \n
    if (n <= 0)
        exit(0);
    
    char name[n];
    int graph[n][n];
    
    for(int i=0; i<n; i++){
        for(int j=0; j<n; j++){
            graph[i][j] = 0;
        }
    }
    
    printf("Enter name ( 1 symb)\n");
    for(int i=0; i<n; i++){
        printf("%d: ",i+1);
        scanf("%c", &name[i]);
        getchar(); //ing \n
        for (int j=0; j<i; j++){
            if( name[i] == name[j]){
                printf("dup name\n");
                i--;
            }
        }

    }
    
    printf("Enter connection:\n");
    for(int i=0; i<n; i++){
        printf("%c: ",name[i]);
        char c;
        int flag = 0;
        while( (c=getchar()) != '\n' ){
            if(c == ' '){
                flag = 0;
            } else if(('a' <= c && c <= 'z') || ('A' <= c && c <= 'Z') || flag == 0){
                for(int j = 0; j<n; j++){
                    if(name[j] == c){
                        graph[i][j]++;
                        j=n;
                    }
                }
                flag = 1;
            }
        }
    }
    
    printf("\n");
    
    int graph_check = 1;
    for(int i=0; i<n; i++){
        int temp_graph_check = 0;
        for(int j=0; j<n; j++){
            if(graph[i][j] == 1)
                temp_graph_check = 1;
    
            if(graph[j][i] == 1)
                temp_graph_check = 1;
        }
        if(temp_graph_check == 0)
            graph_check=0;
    }
    if(graph_check == 0){
        printf("unrelated graph\n");
    } else {
        printf("related graph\n");

    }
    printf("--------------------\n");

    for(int i=0; i<n; i++) {
        printf("%c | ", name[i]);
        for (int j=0; j<n; j++) {
            printf("%d  ", graph[i][j]);
        }
        printf("\n");
    }
    
    search(n, graph, name);
    
    FILE *f = fopen("graph.dot", "w");
    if(f == NULL) {
        printf("Unable to create file\n");
        exit(0);
    }
    char arr[3] = "->";
    fputs("digraph G {", f);
    for(int i=0; i<n; i++){
        char temp_name[2];
        temp_name[0]=name[i];
        fputs(temp_name, f);
        fputs("; ", f);
    }
    for(int i=0; i<n; i++){
        for(int j=0; j<n; j++){
            for(int k=0; k<graph[i][j]; k++){
                char temp_name[2] = {0};
                temp_name[0]=name[i];
                fputs(temp_name, f);
                
                fputs(arr, f);
                
                temp_name[0]=name[j];
                fputs(temp_name, f);
                fputs("; ", f);
            }
        }
    }
    fputs("}", f);
    fclose(f);
    return 0;
}
