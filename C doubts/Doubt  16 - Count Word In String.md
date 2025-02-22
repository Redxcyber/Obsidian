
```c
//write a program to enter a text and then count no of times the a specific word is repeated in the text


#include<stdio.h>
int main(){
    char text[100], word[20];
  
    //input strings
    printf("Enter a text string : ");
    fgets(text, sizeof(text), stdin);
    printf("Enter a word of text string : ");
    fgets(word, sizeof(word), stdin);
  
    //remove newline char
    for(int i=0; text[i] != '\0'; i++){
        if(text[i]=='\n'){
            text[i]='\0';
        }
    }
    for(int i=0; word[i] != '\0'; i++){
        if(word[i]=='\n'){
            word[i]='\0';
        }
    }
  
    //search number of times word appeared
    int i,j,count=0;
    for(i=0; text[i] != '\0'; i++){
        for(j=0; text[i+j]==word[j] && word[j] != '\0'; j++);
        if (word[j] == '\0') {
            count++;
        }
    }
  
    //output count
    printf("Number of times \"%s\" found = %d",word,count);
    return 0;
}
```

##### Problem
```c
Enter a text string : i ii i ii
Enter a word of text string : i
Number of times "i" found = 6
```

#### Solution

```c
//write a program to enter a text and then count no of times the a specific word is repeated in the text


#include<stdio.h>
int main(){
    char text[100], word[20];
  
    //input strings
    printf("Enter a text string : ");
    fgets(text, sizeof(text), stdin);
    printf("Enter a word of text string : ");
    fgets(word, sizeof(word), stdin);
  
    //remove newline char
    for(int i=0; text[i] != '\0'; i++){
        if(text[i]=='\n'){
            text[i]='\0';
        }
    }
    for(int i=0; word[i] != '\0'; i++){
        if(word[i]=='\n'){
            word[i]='\0';
        }
    }
  
    //search number of times word appeared
    int i,j,count=0;
    for(i=0; text[i] != '\0'; i++){
        for(j=0; text[i+j]==word[j] && word[j] != '\0'; j++);

        // If we found a full match of `word`:
        if (word[j] == '\0') {
            // Ensure the match is a full word:
            if ((i==0 || text[i-1] == ' ') && (text[i+j] == ' ' || text[i+j] == '\0')) { // Start at a bounday && Ends at a boundary
                count++;
            }
        }
    }
  
    //output count
    printf("Number of times \"%s\" found = %d",word,count);
    return 0;
}
```

