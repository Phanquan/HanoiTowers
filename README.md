# HanoiTowers
## Giới Thiệu:
Sử dụng thư viện d3js để vẽ hình và tạo animation chuyển động cho các đĩa.  
Sử dụng Lập trình hướng đối tượng (JavaScript ES6) để giải quyết thuật toán của bài toán Tháp Hà Nội.  

## Logic  
#### Sử dụng thuật toán Đệ Quy để giải quyết bài toán:  
```
var hanoi = function(disc,src,aux,dest){
  if(disc > 0){
    hanoi(disc -1,src,dest,aux);
    console.log('Move disc '+disc+' from '+src+' to '+dest);
    hanoi(disc -1,aux,src,dest);
  }
};
hanoi(3,'src','aux','dest');
```
#### Trong đó:    
* src,aux,dest là các Tháp tương ứng: Tháp gốc (src),Tháp trung gian(aux) và Tháp Đích.
* disk là tham số dạng Number tương ứng số đĩa truyền vào.
#### Cách giải  
* Chuyển n-1 đĩa từ cọc A sang B. Chỉ còn đĩa n trên cọc A.  
* Chuyển đĩa n từ cọc A sang cọc C.  
* Chuyển n-1 đĩa từ B sang C cho các đĩa có đường kính nhỏ hơn lần lượt nằm trên đĩa n.  
* Dùng thuật đệ quy để giải quyết bài toán này, tiến hành bước 1 và 3, áp dụng lại thuật giải cho n-1.  
## Animation

