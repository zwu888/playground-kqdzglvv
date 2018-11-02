# 

```C++ runnable
int x,y; // globals
class enclose { // 外围类
    private:
        int x; // 注意：私有成员
    protected:
        int xx;
    public:
        int xxx;
    private:
        static int s;
    public:
        private:
        struct inner { // 嵌套类
            void f(int i) {
               //x = i; // 错误：不能不带实例地写入非静态的 enclose::x
                //xx = i;
                //xxx = i;
                int a = sizeof x; // C++11 前错误。
                                  // C++11 中 OK ： sizeof 的运算数不求值，
                                  // 非静态 enclose::x 的此使用是允许的。
                s = i;   // OK ：能赋值给静态 enclose::s
                ::x = i; // OK ：能赋值给全局 x
                y = i;   // OK ：能赋值给全局 y
            }
            void g(enclose* p, int i) {
                p->x = i; // OK ：赋值给 enclose::x
                p->xx = i;
                p->xxx = i;
            }
        };
};

int main()
{
    return 0;
}
