# HanoiTowers
## Giới Thiệu:
Sử dụng thư viện d3js để vẽ hình và tạo animation chuyển động cho các đĩa.  
Sử dụng Lập trình hướng đối tượng (JavaScript ES6) để giải quyết thuật toán của bài toán Tháp Hà Nội.  

## Logic  
#### Sử dụng thuật toán Đệ Quy để giải quyết bài toán:  
```javascript
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
* Class Disk chứa các thuộc tính của Đĩa và phương thức draw để vẽ đĩa:
```javascript
class Disk {
	constructor(nameDisks, d) {   //tham số truyền vào
		this.name = nameDisks //Định nghĩa thuộc tính tên Đĩa cho class Disk
		this.diameter = d     //Định nghĩa thuộc tính số thứ tự hay bán kính,các đĩa có bán kính lớn hơn thì ở dưới
	}
	drawDisk(...) {
		//phương thức vẽ
	}
}
```
* Class Tower chứa các thuộc tính của Tower và phương thức draw để vẽ tower:
```javascript
class Tower {
	constructor(nameTowers, arrDisk) { //tham số truyền vào
		this.name = nameTowers //Định nghĩa thuộc tính Tên Tháp
		this.arrDisk = arrDisk //Định nghĩa thuộc tính mảng chứa các Đĩa
	}
	drawTower(...) {
		//phương thức vẽ
	}
}
```
* Class GameEngine chứa logic xử lý bài toán:
```javascript
class GameEngine {
	constructor() {
		this.count = 0 //đếm các bước thực hiện bài toán
		this.data = [] //Định nghĩa thuộc tính data là mảng chứa các step ở dưới.Ta sẽ tạo animation thông qua data.
		this.step = {} //Định nghĩa thuộc tính step là đối tượng, tức các bước di chuyển của đĩa qua các tháp
	}

	//Phương thức để giải quyết bài toán tháp hà nội
	move(n, a, b, c) {
		if (n > 0) {
			this.move(n - 1, a, c, b)
			console.log(`Move disk ${n} from ${a.name} to ${c.name}`);
			
			//Ta định nghĩa các thuộc tính diskToPick,fromTower,toTower cho đối tượng step.
			this.step = {
				diskToPick: diskArr[n - 1], //current disk
				fromTower: a, //fromTower
				toTower: c //toTower
			}
			//Ta sẽ đẩy step vào mảng data sau mỗi lần lặp
			this.data.push(this.step) 
			this.count++; //cout the count
			this.move(n - 1, b, a, c)
		}
	}
	
	animateDisk(...) {
		//phương thức animation
	}
}
```
## Animation

