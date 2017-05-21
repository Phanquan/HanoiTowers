# Hanoi Towers
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
## Sử dụng Class trong JSES6 để lập trình OOP giải quyết bài toán Tháp Hà Nội
### Bước 1: Giải quyết thuần Logic thông qua console.log 
* Chia bài toán ra 3 class: Class Disk,class Tower và Class GameEngine để chạy chương trình.  
* Class Disk chứa các thuộc tính của Đĩa:
```javascript
class Disk {
	constructor(nameDisks) {   //tham số truyền vào
		//Định nghĩa thuộc tính tên Đĩa cho class Disk
		this.name = nameDisks  
		
	}
}
```
* Class Tower chứa các thuộc tính của Tower:
```javascript
class Tower {
	constructor(nameTowers) { //tham số truyền vào
		//Định nghĩa thuộc tính Tên Tháp
		this.name = nameTowers
	}
}
```
* Class GameEngine chứa logic xử lý bài toán:
```javascript
class GameEngine {
	constructor() {
		//đếm các bước thực hiện bài toán
		this.count = 0
	}

	//Phương thức để giải quyết bài toán tháp hà nội
	move(n, a, b, c) {
		if (n > 0) {
			this.move(n - 1, a, c, b)
			console.log(`Move disk ${n} from ${a.name} to ${c.name}`);
			this.count++; //count the count
			this.move(n - 1, b, a, c)
		}
	}
}
```
* Khai báo các Instances (hình mẫu) của Đối tượng Disk,Tower,GameEngine và chạy chương trình:
```javascript
let diskArr = [ //Khởi tạo mảng các đĩa
	new Disk('disk1'),
	new Disk('disk2'),
	new Disk('disk3'),
	new Disk('disk4')
]

let towerArr = [ //Khởi tạo mảng các tower
	new Tower('tower1'),
	new Tower('tower2'),
	new Tower('tower3')
]

// Khởi tạo intance game của object GameEngine.
let game = new GameEngine()
console.log(`Truyền vào ${diskArr.length} Đĩa`)

//Chạy logic đệ quy với tham số diskArr.length là số lượng phần tử trong mảng,tower[0->2] là các tower src,aux,dest
game.move(diskArr.length, towerArr[0], towerArr[1], towerArr[2])

console.log(`Tổng cộng ${game.count} bước`)
```
* Cuối cùng là Kết Quả in ra Console:
```
Truyền vào 4 Đĩa

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
### Bước 2: Thêm biến data cho class GameEngine để lưu lại các bước thực hiện bài toán
* Thuộc tính data và ý nghĩa:
	>Thuộc tính data sẽ là mảng gồm các đối tượng,mỗi đối tượng tương ứng một hành động chuyển đĩa từ tower này sang tower khác,nên data sẽ chứa các đối tượng có thuộc tính sau:{disk,fromTower,toTower}.  
	>Ta gọi nó là step (bước thực hiện),sau mỗi lần sử lý logic,ta sẽ 'đẩy' (push) một step vào mảng data.
```javascript
class GameEngine {
	constructor() {
		//đếm các bước thực hiện bài toán
		this.count = 0
		//định nghĩa thuộc tính (property) data dạng mảng
		this.data = []
		//định nghĩa thuộc tính step dạng đối tượng
		this.step = {}
	}

	//Phương thức để giải quyết bài toán tháp hà nội
	move(n, a, b, c) {
		if (n > 0) {
			this.move(n - 1, a, c, b)
			console.log(`Move disk ${n} from ${a.name} to ${c.name}`);
			//tượng tự console.log ở trên,ta gán tham số cho step rồi đẩy vào mảng data
			this.step = {
				diskToPick: diskArr[n-1], //đĩa sẽ chọn(n-1 là do diskArr ở dạng mảng)
				fromTower: a,    //truyền vào tower1
				toTower: c	//gán cho tower3
			}
			// sau khi gán thuộc tính cho step thì đẩy vào data
			this.data.push(this.step)
			this.count++; //count the count
			this.move(n - 1, b, a, c)
		}
	}
}
```
* Khi console.log data ta sẽ có kết quả như sau:
```javascript
console.log(game.data)//log ra thuộc tính data của instance game.

[ { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower1' },
    toTower: Tower { name: 'tower2' } },
  { diskToPick: Disk { name: 'disk2' },
    fromTower: Tower { name: 'tower1' },
    toTower: Tower { name: 'tower3' } },
  { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower2' },
    toTower: Tower { name: 'tower3' } },
  { diskToPick: Disk { name: 'disk3' },
    fromTower: Tower { name: 'tower1' },
    toTower: Tower { name: 'tower2' } },
  { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower3' },
    toTower: Tower { name: 'tower1' } },
  { diskToPick: Disk { name: 'disk2' },
    fromTower: Tower { name: 'tower3' },
    toTower: Tower { name: 'tower2' } },
  { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower1' },
    toTower: Tower { name: 'tower2' } },
  { diskToPick: Disk { name: 'disk4' },
    fromTower: Tower { name: 'tower1' },
    toTower: Tower { name: 'tower3' } },
  { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower2' },
    toTower: Tower { name: 'tower3' } },
  { diskToPick: Disk { name: 'disk2' },
    fromTower: Tower { name: 'tower2' },
    toTower: Tower { name: 'tower1' } },
  { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower3' },
    toTower: Tower { name: 'tower1' } },
  { diskToPick: Disk { name: 'disk3' },
    fromTower: Tower { name: 'tower2' },
    toTower: Tower { name: 'tower3' } },
  { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower1' },
    toTower: Tower { name: 'tower2' } },
  { diskToPick: Disk { name: 'disk2' },
    fromTower: Tower { name: 'tower1' },
    toTower: Tower { name: 'tower3' } },
  { diskToPick: Disk { name: 'disk1' },
    fromTower: Tower { name: 'tower2' },
    toTower: Tower { name: 'tower3' } } ]
```
* Có thể thấy rằng mỗi phần tử của data sẽ tương ứng với một bước (step dã nêu trên) để thực hiện việc chuyển đĩa,ta sẽ dùng data để mô tả việc nhấc,hạ đĩa qua các tháp.
### Bước 3: Draw và Animation
* Ta sẽ đóng gói các bước vẽ và animation sao cho đĩa sẽ có phương thức vẽ đĩa,tháp sẽ vẽ tháp và GameEngine sẽ làm animation.
* Khai báo các thuộc tính của svg để vẽ ra thẻ svg:
```javascript
const p = { //đây là đối tượng chứa các thuộc tính để vẽ svg
	svgWidth: 1200,		//chiều rộng của svg
	svgHieght: 600,		//chiều cao của svg
	diskHeight: 50,	       	//chiều cao của đĩa
	disNearestTower: 400,  	//khoảng  cách giữa 2 tower gần nhất
	disFurthestTower: 800, 	//khoảng cách giữa 2 tower xa nhất
	towerBuffer: 100,      	//tham số để chia khoảng trắng giữa giữa 2 tower 
	animationDelay: 3000,  	//=thời gian delay của animation
	animationDuration: 1000	//=thời gian chuyển động của animation
};

const svg = d3.select('body') 			//chọn thẻ body
		.append('svg') 			//tạo thêm thẻ svg
		.attr('width',p.svgWidth) 	//với thuộc tính width
		.attr('height',p.svgHieght) 	//với thuộc tính height
```
* Thêm phương thức vẽ đĩa,tháp:  
	>Disk
```javascript
class Disk {
	constructor(nameDisks,d) {   //tham số truyền vào
		//Định nghĩa thuộc tính tên Đĩa cho class Disk
		this.name = nameDisks
		this.diameter = this.d  //STT		
	}
	drawDisk(svgInput, attrX, attrY, attrWidth, attrHeight, attrClass){//tham số
		svgInput.append('rect')
			.attr('x', attrX)
			.attr('y', attrY)
			.attr('width', attrWidth)
			.attr('height', attrHeight)
			.attr('class', attrClass)
	}
}
```
	> Tower
```javascript
class Tower {
	constructor(nameTowers,arrOfDisk) { //tham số truyền vào
		//Định nghĩa thuộc tính Tên Tháp
		this.name = nameTowers
		//mảng của tower chứa các disk,khi bắt đầu,tower 1 sẽ chứa n đĩa,các tower còn lại rỗng
		this.arrOfDisk = arrOfDisk 
	}
	drawTower(svgInput, attrX1, attrY1, attrX2, attrY2) { //tham số
		//sử dụng inser thay cho append để tạo thẻ line cho tower ko đè lên disk
		svgInput.insert('line', ':first-child')
			.attr('x1', attrX1)
			.attr('y1', attrY1)
			.attr('x2', attrX2)
			.attr('y2', attrY2)
			.attr('stroke-width', 10)
			.attr('stroke', 'black');
	}
}
```
* Ta sẽ viết lại cách khai báo Instances ở trên:
```javascript
let numberOfDisk = 3		//tạm thời khai báo số lượng đĩa = 3.
const numberOfTower = 3		//khai báo số lượng tháp,luôn bằng 3.
let diskArr = []		//khai báo mảng chứa đĩa.
let towerArr = []		//khai báo mảng chứa tháp.

for (var j = 1,j <= numberOfDisk,j++){
	//Định nghĩa một instance của Disk với tham số disk1,2,3 và stt
	diskArr.push(new Disk('disk' + j, j))

	//sử dụng phương thức drawDisk để vẽ đĩa,diskArr[j-1] nghĩa là phần tử thứ j-1 trong mảng diskArr
	diskArr[j - 1].drawDisk(
		svg, 								//svg argument
		(numberOfDisk - j) * p.diskHeight / 2 + p.diskHeight * 2, 	//.attr('x',
		j * p.diskHeight + 2 * p.diskHeight, 				//attr('y',
		j * p.diskHeight, 						//.attr('width',
		p.diskHeight, 							//.attr('height',
		'color disk' + j, 						//.attr('class',
	)
}

for (var j = 1; j <= numberOfTower; j++) {
	//define new 3 towers
	if (j - 1 === 0) {
		towerArr.push(new Tower('tower' + j, diskArr)) 	// đẩy mảng disk vào tower đầu tiên
	} else {
		towerArr.push(new Tower('tower' + j, [])) 	//các tower còn lại ko có gì
	}
	//tương tự vẽ đĩa khi vẽ tower 
	towerArr[j - 1].drawTower(
		svg, 							//svg argument
		p.towerBuffer + (numberOfDisk * p.diskHeight) / 2, 	//attr x1
		120, 							//attr x2
		p.towerBuffer + (numberOfDisk * p.diskHeight) / 2, 	//attr y1
		numberOfDisk * p.diskHeight + 150 			//attr y2
	)
	p.towerBuffer += 400 //sau mỗi vòng lặp thì tăng khoảng cách giữa các tower lên
}
p.towerBuffer = 100 //reset lại buffer
//đặt màu random cho đĩa
d3.selectAll('.color').style('fill', function() {
	return `hsl( ${Math.random() * 360}  ,100%,50%)`
});
```
* Kết quả với numberOfDisk = 3:
<img src="http://imgur.com/YwvSjpI">
* Kết quả với numberOfDisk = 4:
<img src="http://imgur.com/qTrDPmF">
