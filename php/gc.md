#### unset
unset只是断开一个变量到一块内存区域的链接,同时将该区域的引用计数-1,内存是否回收主要看refcount是否为0