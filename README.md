![image](https://www.img.in.th/images/43786daea07df32abdd38bb4ac6fe492.png)


SQL
1.จงหาจำนวนคนแต่ละแผนก
select DepartmentName,COUNT(Employees.EmployeeID) 
from Employees,Departments
where Employees.departmentID =  Departments.departmentID
group by DepartmentName;

2.จงหาข้อมูลพนักงานทุกคนเรียงตามแผนกถ้าคนที่ไม่มีแผนกให้แสดงข้อความว่า “ไม่มีแผนก” ที่คอมลัมชื่อแผนก
select case DepartmentName when isnull then 'ไม่มีแผนก' else DepartmentName end  ,EmployeeID,Fname,Lname,Brithday,age,Tel
from Employees,Departments
where Employees.departmentID = Departments.departmentID
order by DepartmentName asc;

3. จงหาข้อมูลหัวหน้าแผนกแต่ละแผนก
select DepartmentName,LevelName,EmployeeID,Fname,Lname,Brithday,age,Tel
from Employees,Departments,Levels
where Employees.departmentID = Departments.departmentID 
and Levels.LevelID = Employees.LevelID 
and LevelName = 'PM'
order by DepartmentName asc;

4. หาหัวหน้าแผนก ของแผนกแต่ละแผนกที่จำนวนคนมากที่สุด
select Fname
from Employees,Departments,Levels
where Employees.departmentID = Departments.departmentID 
and Levels.LevelID = Employees.LevelID 
and LevelName = 'PM'
group by Fname
having Count(EmployeeID) = MAX(EmployeeID);
