package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

@Controller	
@RequestMapping(path="/")
public class MainController {

    @Autowired
    private CursoRepository repository;

    @GetMapping(path="/")
    public @ResponseBody String home () {
        return "Quezada - Alfred Jerico Huarcaya";
    }

    @GetMapping(path="/codigo")
    public @ResponseBody String codigo () {
        return "Quezada";
    }

    @GetMapping(path="/nombre-completo")
    public @ResponseBody String nombre () {
        return "Alfred Jerico Huarcaya";
    }
    
    @PostMapping(path="/api/curso/nuevo")
    public @ResponseBody String nuevo (@RequestParam String nombre, @RequestParam Integer creditos) {
        Curso n = new Curso();
        n.setNombre(nombre);
        n.setCreditos(creditos);
        repository.save(n);
        return "Curso Guardado";
    }

    @DeleteMapping(path="/api/curso/eliminar")
    public @ResponseBody String eliminar (@RequestParam Integer id) {
        repository.deleteById(id);
        return "Curso Eliminado";
    }

    @GetMapping(path="/api/curso/listar")
    public @ResponseBody Iterable<Curso> listar() {
        return repository.findAll();
    }
}