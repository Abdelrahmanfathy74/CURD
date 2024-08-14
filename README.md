# CURD
crud java 
//
=======================================for class TODO============
package home;

import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;
import lombok.Setter;

import javax.persistence.*;

@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name = "todos")
public class TODO {
    @Id
    @Column
    private int id ;
    @Column(name = "fullname")
    private String name;
    @Column(name = "email_id")
    private String message;




/*public TODO(){}
    public TODO(long id, String name, String message ) {
        this.id = id;
        this.name = name;
        this.message = message;
    }

    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }*/}



===================================for   "Main"==================
package home;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class App  {
    @Autowired
    TodosRepository todosRepository;
    public static void main( String[] args )
    {
        SpringApplication.run(App.class, args);

    }

    /*	@Override
	public void run(String... args) throws Exception {
		TODO todo=new TODO();
		todo.setId(1);
		todo.setName("abdofathy");
		todo.setMessage("body75099@gmail.com");
            todosRepository.save(todo);

		TODO todo1=new TODO();
		todo.setId(2);
		todo.setName("ayafathy");
		todo.setMessage("aya@gmail.com");
            todosRepository.save(todo1);

	}*/
}
================================================for controller============================
package home;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/abdo/fathy")
public class TodoController {

    @Autowired
   // private TodoService todoservice;
private TodosRepository todosrepository;

    @GetMapping({"","/"})
    public List<TODO> getallemp(){
    return todosrepository.findAll();

    }
    /*@GetMapping("/{id}")
    public TODO getid(@PathVariable("id") long id){
        return todoservice.getbyid(id);
    }
    @PostMapping({"","/"})
    public TODO createnewtodo(@RequestBody TODO todo){
       return todoservice.save(todo);
    }
    @DeleteMapping("/{id}")
    public void deletetodo(@PathVariable long id){
        todoservice.remove(id);
    }*/
=
    @PostMapping
    public TODO createmewtodo(@RequestBody TODO todo){

 =       return todosrepository.save(todo);
    }

=
    @GetMapping("/{id}")
    public ResponseEntity<TODO> getbyid(@PathVariable int id)
    {
        TODO todo= todosrepository.findById(id)
                .orElseThrow(()->new RuntimeException("employee is not found by id"+id));
        return ResponseEntity.ok(todo);
    }
    @PutMapping("{id}")
    public ResponseEntity<TODO> updatetodo(@PathVariable int id,@RequestBody TODO tododetials){
        TODO todo=todosrepository.findById(id)
                .orElseThrow(()->new RuntimeException("employee is not found by id "+id));
        todo.setId(tododetials.getId());
        todo.setName(tododetials.getName());
        todo.setMessage(tododetials.getMessage());
         todosrepository.save(todo);
         return ResponseEntity.ok(todo);
    }
    @DeleteMapping("{id}")
    public ResponseEntity<TODO> deletetodo(@PathVariable int id){
        TODO todo=todosrepository.findById(id)
                .orElseThrow(()-> new RuntimeException("message is not found by id"+id));
        todosrepository.delete(todo);
    return new ResponseEntity<>(HttpStatus.NO_CONTENT);

    }

}

================================for TodosService =================================
package home;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

@Service
@RequestMapping("/id")
public class TodoService {
/*


    @Autowired
    private TodosRepository todosRepository;


    public List<TODO> findall() {
        return todosRepository.findAll();
    }

    public TODO getbyid(long id){
      return todosRepository.findById(id).get();
    }
   */
/* public TODO save(TODO todo){
        return todosRepository.insert(todo);
    }
   *//*
 public void remove(long id){
     todosRepository.deleteById(id);   }
*/

        }
=============================== for interface TodosRepository========================
package home;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface TodosRepository extends JpaRepository<TODO,Integer> {
}
======================================================================================
