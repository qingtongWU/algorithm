~~~c
class Solution {
public:
    int strStr(string haystack, string needle) {
         int len=needle.size();
        if(len==0)
            return 0;
        if(haystack.size()==0||haystack.size()<len)
            return -1;
        int n;//用来记录匹配成功，匹配的位置
        for(int i=0;i<haystack.size();i++){ 
                if(needle[0]== haystack[i]){//匹配开始
                    n=i;//更新位置
                    for(int j=0;j<len;j++){
                        if(needle[j]!=haystack[i+j])//匹配失败
                            break;
                        if(j==len-1)//匹配成功
                            return n;
                     }
                 }    
         }
        return -1;
    } 
};
~~~

