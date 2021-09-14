~~~c
class LRUCache {
public:
    //有参构造函数
    LRUCache(int capacity) 
    :_capacity(capacity)
    { }
    
    //获取key对应的value
    int get(int key) 
    {
        auto it = _map.find(key);//key所在位置的迭代器

        if(it != _map.end())//key是存在的
        {
            _lst.splice(_lst.begin(),_lst,it->second);//刚被访问过的元素移动到链表的头部
            return it->second->second;
        }
        return -1;//key不存在，返回-1
    }
    
    //存入键值对
    void put(int key, int value) 
    {
        auto it = _map.find(key);
        if(it != _map.end())//要修改的值存在
        {
            _lst.splice(_lst.begin(),_lst,it->second);//刚被访问过的元素移动到链表的头部
            it->second->second = value;
            return;
        }

        _lst.emplace_front(key,value);//插入链表头部
        _map[key] = _lst.begin();//插入_map头部

        //缓存容量已经满了，需要删除内容空出位置
        if(_map.size() > _capacity)
        {
            _map.erase(_lst.back().first);
            _lst.pop_back();
        }
    }

private:
    size_t _capacity;//unordered_map的容量
    unordered_map<int,list<pair<int,int>>::iterator> _map;
    list<pair<int,int>> _lst;//因为双向链表中要存key和value,所以用pair类型
};
~~~

