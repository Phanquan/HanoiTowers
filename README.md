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
* Tiến hành bước 1 và 3, áp dụng lại thuật giải cho n-1.  
#### Kết quả in ra Console.log: 
```
Truyền vào 4 đĩa

Move disk 1 from tower1 to tower2  js.js:51:4
Move disk 2 from tower1 to tower3  js.js:51:4
Move disk 1 from tower2 to tower3  js.js:51:4
Move disk 3 from tower1 to tower2  js.js:51:4
Move disk 1 from tower3 to tower1  js.js:51:4
Move disk 2 from tower3 to tower2  js.js:51:4
Move disk 1 from tower1 to tower2  js.js:51:4
Move disk 4 from tower1 to tower3  js.js:51:4
Move disk 1 from tower2 to tower3  js.js:51:4
Move disk 2 from tower2 to tower1  js.js:51:4
Move disk 1 from tower3 to tower1  js.js:51:4
Move disk 3 from tower2 to tower3  js.js:51:4
Move disk 1 from tower1 to tower2  js.js:51:4
Move disk 2 from tower1 to tower3  js.js:51:4
Move disk 1 from tower2 to tower3  js.js:51:4

Tổng cộng 15 bước
```
## Sử dụng Class trong JSES6 để lập trình OOP giải quyết bài toán Tháp Hà Nội
#### Chia Bài toán ra 3 Class: 
* Class Disk,class Tower và Class GameEngine để chạy chương trình.  
* Class Disk chứa các thuộc tính của Đĩa và phương thức draw để vẽ đĩa  
```
class Disk {
	constructor(nameDisks, d) {
		this.name = nameDisks
		this.diameter = d
	}
	drawDisk(...) {
		//code to draw
	}
}
```
* Class Tower chứa các thuộc tính của Tower và phương thức draw để vẽ tower  
```
class Tower {
	constructor(nameTowers, arrDisk) {
		this.name = nameTowers //Tên Tháp
		this.arrDisk = arrDisk //mảng chứa các Đĩa
	}
	drawTower(svgInput, attrX1, attrY1, attrX2, attrY2) {
		//code to draw towers
	}
}
```

## Animation

