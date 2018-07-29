# C++ Tips

# シングルトンの実装

singletonclass.h

```cpp {.line-numbers}
class SingletonClass
{
public:
    static const std::unique_ptr<SingletonClass>& instance();

private:
    SingletonClass() = default;
public:
    virtual ~SingletonClass() = default;

    SingletonClass( const SingletonClass& ) = delete;
    SingletonClass( SingletonClass&& ) = delete;
    SingletonClass& operator=( const SingletonClass& ) = delete;
    SingletonClass& operator=( SingletonClass&& ) = delete;

public:
    std::string name() const;
    int count() const;
public:
    void countUp();

private:
    std::string m_name = "undefined";
    int m_count = 0;
};
```

singletonclass.cpp

```cpp {.line-numbers}
const std::unique_ptr<SingletonClass>& SingletonClass::instance()
{
    // privateコンストラクタのため、make_uniqueでは生成できない
    //static auto&& instance = std::make_unique<SingletonClass>();

    // 同一クラス内なので、newは可能
    //static std::unique_ptr<SingletonClass> instance( new SingletonClass() );

    // make_uniqueで生成できるようにするため、ローカルのサブクラス（構造体）を定義する
    // サブクラスを定義する関係上、シングルトンクラスはfinal指定できない
    struct ctor_permission : public SingletonClass
    {
        using SingletonClass::SingletonClass;
    };
    static std::unique_ptr<SingletonClass>&& instance = std::make_unique<ctor_permission>();
    return instance;
}
```
