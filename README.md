# Lista de tareas

Base de datos de ejemplo.

## Modelo entidad relación

![Modelo entidad relación](/docs/model.png)

## Script SQL

```sql

--  *   -----------------------------------------------------------------------
--  *   Database
--  *   -----------------------------------------------------------------------
DROP DATABASE IF EXISTS dbTodoList;
CREATE DATABASE IF NOT EXISTS dbTodoList;
USE dbTodoList;

--  *   -----------------------------------------------------------------------
--  *   Table Lists
--  *   -----------------------------------------------------------------------
DROP TABLE IF EXISTS Lists;
CREATE TABLE IF NOT EXISTS Lists
(
    id          INT         UNSIGNED  NOT  NULL  AUTO_INCREMENT  COMMENT  '',
    name        VARCHAR(65)           NOT  NULL                  COMMENT  '',
    created_at  DATETIME              NOT  NULL  DEFAULT NOW()   COMMENT  '',
    updated_at  DATETIME                   NULL  DEFAULT NULL    COMMENT  '',
    deleted_at  DATETIME                   NULL  DEFAULT NULL    COMMENT  '',
    CONSTRAINT  pk_list       PRIMARY KEY (id),
    CONSTRAINT  uk_id_list    UNIQUE(id ASC) VISIBLE,
    CONSTRAINT  uk_name_list  UNIQUE(name ASC) VISIBLE
)ENGINE = InnoDB
COMMENT = 'Lists';

--  *   -----------------------------------------------------------------------
--  *   Table Tasks
--  *   -----------------------------------------------------------------------
DROP TABLE IF EXISTS Tasks;
CREATE TABLE IF NOT EXISTS Tasks
(
    id           INT           UNSIGNED  NOT  NULL  AUTO_INCREMENT   COMMENT  '',
    list_id      INT           UNSIGNED       NULL  DEFAULT   1      COMMENT  '',
    title        VARCHAR(120)            NOT  NULL                   COMMENT  '',
    description  VARCHAR(512)                 NULL  DEFAULT   NULL   COMMENT  '',
    completed    TINYINT                 NOT  NULL  DEFAULT   0      COMMENT  '',
    created_at   DATETIME                NOT  NULL  DEFAULT   NOW()  COMMENT  '',
    updated_at   DATETIME                     NULL  DEFAULT   NULL   COMMENT  '',
    deleted_at   DATETIME                     NULL  DEFAULT   NULL   COMMENT  '',
    CONSTRAINT pk_tasks        PRIMARY KEY (id),
    CONSTRAINT uk_id_tasks     UNIQUE(id ASC) VISIBLE,
    CONSTRAINT fk_tasks_lists  FOREIGN KEY (list_id)
        REFERENCES Lists (id) ON DELETE NO ACTION ON UPDATE NO ACTION
)
ENGINE = InnoDB
COMMENT = 'List tasks';

--  *   -----------------------------------------------------------------------
--  *   Inserts Table Lists
--  *   -----------------------------------------------------------------------
INSERT INTO Lists(name, created_at)
VALUES
    ('Todos', NOW());

--  *   -----------------------------------------------------------------------
--  *   Inserts Table Tasks
--  *   -----------------------------------------------------------------------
INSERT INTO Tasks(list_id, title, description, completed, created_at)
VALUES
    (1, 'predeterminado', NULL, true, NOW());

```
