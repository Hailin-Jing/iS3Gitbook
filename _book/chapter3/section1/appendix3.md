# 主键

`Entity Framework Code First`的默认主键约束：*属性名为[ID]或[类名 + ID]*。如在`Product`类中，`Entity Framework Code First`会根据默认约定将类中名称为`ID`或`ProductID`的属性设置为主键。`Entity Framework Code First`主键的默认约定也一样可以进行重写，重新根据需要进行设置。

## Data Annotation 方式

```csharp
    using System.ComponentModel.DataAnnotations;
    using System.ComponentModel.DataAnnotations.Schema;
    [Key]
    [Column("ProductID")]
    public int ProductID { get; set; }
```

## Fluent API方式

```csharp
    protected override void OnModelCreating(DbModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Product>().HasKey(t => t.ProductID);
    }
```

若一个表有多个主键时：

```csharp
    protected override void OnModelCreating(DbModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Product>().HasKey(t => new { t.KeyID, t.CandidateID });
    }[Column("UnitPrice", TypeName = "MONEY")]
public decimal UnitPrice { get; set; }
```
