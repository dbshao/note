指定扫描路径后，并不是该路径下所有组件类都扫描，只有在组件类定义前面有以下注解标记时，才会扫描到spring容器

####通用注解
@Name @Component
####持久化注解
@Repository
####业务层注解
@Service
####控制层注解
@Controller

噹注解被扫描到时，会生成一个默认的id值，改id为小写开头的类名，可以在注解标记中自定义id

####初始化和销毁的回调控制
@PostConstruct 用于初始化回调 方法 init（）
@PreDestroy 用于销毁回调方法 destroy（）

####依赖关系
具有依赖关系的Bean对象可以用下面任意一个实现关系注入
@Resource
@Autowired、@Qualifier
@Inject、@Named

@Resource注解标记可以用在字段定义或者setter方法定义前面，默认首先按照名称匹配来注入，然后类型匹配注入

当遇到多个Bean时会发生错误，可以显示指定名称来表明
例如@Resource（name=“”）









