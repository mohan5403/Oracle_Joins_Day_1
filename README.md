-- Oracle_Joins_Day_1
-- from oracle live sql 
-- Link is https://livesql.oracle.com/

create table emp_1 as select * from scott.emp;

create table dept_1 as select * from scott.dept;


select d.dname, count(d.deptno) as Count_dept from emp_1 e, dept_1 d where e.deptno = d.deptno group by d.dname;

select * from emp_1;

select * from dept_1;

select d.loc, extract(year from e.hiredate) as year_1, count(*) from emp_1 e, dept_1 d where d.deptno = e.deptno 
group by d.loc, extract(year from e.hiredate)
order by year_1;

select * from salgrade;

select e.empno, e.ename, e.sal, s.grade, d.deptno from emp_1 e, salgrade s, dept_1 d where e.deptno = d.deptno 
and
e.sal between s.losal and s.hisal;

select *  from emp_1 e RIGHT OUTER JOIN DEPT_1 d on e.deptno = d.deptno;
select * from emp_1 e, dept_1 d where e.deptno = d.deptno(+);

select * from emp_1 e full outer join dept_1 d on e.deptno = d.deptno where job = 'MANAGER';

select * from emp_1 e, dept_1 d where e.deptno(+) = d.deptno and job = 'MANAGER'
union 
select * from emp_1 e, dept_1 d where e.deptno = d.deptno(+) and job = 'MANAGER';

select m.ename as "Mangaer Name",
       m.job,
       m.sal as "Manager Salary" ,
       e.ename as "Employee Name", 
       e.job, 
       e.sal as "Employee Salary"
from emp_1 e, emp_1 m
where 
    e.mgr = m.empno
and 
    e.sal > m.sal;

select m.ename as "Mangaer Name",
       m.job,
       m.sal as "Manager Salary" ,
       e.ename as "Employee Name", 
       e.job, 
       e.sal as "Employee Salary"
from emp_1 e, emp_1 m
where 
    e.mgr = m.empno
and 
    e.hiredate < m.hiredate;

select * from (select count(*) as records_1 from emp_1) ;

select * from dept_1 natural join  emp_1;   

select * from emp_1 join dept_1 using(deptno);

select * from emp_1 e inner join dept_1 d on e.deptno = d.deptno;
--select * from emp_1 d inner join dept_1 e on e.deptno = d.deptno;

select * from dept_1 d cross join emp_1 e where e.job ='MANAGER';

select  job, deptno d from emp_1 where deptno = 10 
union all
--union
select job j, deptno from emp_1 where deptno = 20 order by 2,1;
