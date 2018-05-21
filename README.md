หาปีที่มีวันเสาร์ วันจันทร์ วันอาทิตย์ที่มี 5วันในเดือนมกราคม
int Ystart = 2500 - 543;
            int Yend = 2600 - 543;
            int count = 0;
            for (int y = Ystart; y <= Yend; y++)
            {
                DateTime date = new DateTime(y, 1, 1);
                var sat = Enumerable.Range(0, 31).Where(x => date.AddDays(x).DayOfWeek == DayOfWeek.Saturday).Count();
                var sun = Enumerable.Range(0, 31).Where(x => date.AddDays(x).DayOfWeek == DayOfWeek.Sunday).Count();
                var mon = Enumerable.Range(0, 31).Where(x => date.AddDays(x).DayOfWeek == DayOfWeek.Monday).Count();
                if(sat == 5 && sun == 5 && mon == 5)
                {
                    ViewBag.yearselect += y +543+ " ";
                    count += 1;
                    ViewBag.counting = count;
                }
            }
---------------------------------------------------------------            
             int sYe = 2500 - 543;
            int eYe = 2600 - 543;
            for (int YY = sYe; YY < eYe; YY++)
            {
                DateTime dd = new DateTime(YY, 1, 1);
                 if((int)dd.DayOfWeek == 6)
                {
                    ViewBag.datayear += YY + 543+" " ;

                }
            }
--------------------------------------------------------------
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



select TOP 1 e.FName,l.LevelName, d.departmentName,COUNT(e.EmployeeID)as countemployee
from Employees e, Departments d,Levels l
where d.DepartmentID = e.DepartmentID 
and  e.LevelID = l.LevelID 
and l.LevelName = 'PM' 
group by FName,LevelName,departmentName
order by countemployee DESC;
