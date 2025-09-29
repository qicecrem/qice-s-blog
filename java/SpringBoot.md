
@RestController
@RequestMapping("/employee")
public class EmployeeController {
    @Resource
    private EmployeeService employeeService;

    @GetMapping("/selectAll")
    public Result selectAll(){
        List<Employee> list= employeeService.selectAll();
        return Result.success(list);
    }
    //
    @GetMapping("/selectById/{id}")
    public Result selectById(@PathVariable Integer id){
       Employee employee = employeeService.selectById(id);
        return Result.success(employee);
    }
    //
    @GetMapping("/selectOne")
    public Result selectOne(@RequestParam Integer id){
        Employee employee = employeeService.selectById(id);
        return Result.success(employee);
    }
}

get: 查询操作
post 新增操作
put 修改操作
delete 删除操作