<a href="#cvsc">**@Controller VS. @RestController**</a>

---

<p id="cvsc">@Controller VS. @RestController<br>
使用@Controller可配合视图解析器InternalResourceViewResolver直接访问jsp/html页面；<br>
但是使用@RestController[@ResponseBody + @Controller]就不可以跳转视图了；<br>
对于这两者如需在方法中返回json/String都需要在方法上添加@ResponseBody注解</p>