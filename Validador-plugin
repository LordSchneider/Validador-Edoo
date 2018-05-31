<?php
/**
 * Plugin Name: Validador Edoo Help
 * Plugin URI: http://wprincipiante.es
 * Description: Este plugin se asegura de evitar el acceso no autorizado a Edoo Help.
 * Version: 1.0.0
 * Author: Ignacio Casado Schneider
 * Author URI: http://neliosoftware.com
 * Requires at least: 4.0
 * Tested up to: 4.9.6
 *
 * Text Domain: wprincipiante-ejemplo
 * Domain Path: /languages/
 */

    add_action('init',validar);
    add_action('admin_menu',menu);
    add_action('admin_init',edoo_validar_settings);

    function menu(){

        add_menu_page('Ajustes de validador de Edoo','Validador Edoo','administrator','Cambia rick-roleo','bobross','');
    }

    function bobross(){?>

        <div>
            <h2>Cambia valores del validador</h2>
            <form method="POST" action="options.php">
            <?php
                settings_fields('validar_edoo_settings');
                do_settings_sections('validar_edoo_settings');
            ?>
            <label>Sitio a redireccionar: </label>
            <input type="text" name="edoo_validar_sitio_redirect" id="edoo_validar_sitio_redirect" value="<?php echo get_option('edoo_validar_sitio_redirect');?>"/>
            <?php  
                submit_button();
            ?>
            </form>
        </div>
        <?php
    }

    function edoo_validar_settings(){

        register_setting('validar_edoo_settings','edoo_validar_sitio_redirect','strval');
    }

    function validar() {
            
        if (!((isset($_COOKIE['edoouid'])) and (isset($_COOKIE['edoosid'])) and (isset($_COOKIE['edootimestamp'])) and (isset($_COOKIE['edootoken'])))) {    
            $time = $_GET['timestamp'];
            $user = $_GET['uid'];
            $school = $_GET['sid'];
            $token = $_GET['token'];
            $check_token = $time.$user.$school;
            $check_token = md5($check_token);
            if ($check_token === $token) {
                setcookie('edoouid', $user);
                setcookie('edoosid', $school);
                setcookie('edootimestamp', $time);
                setcookie('edootoken', $check_token);
            } else {
                $local=get_option('edoo_validar_sitio_redirect');
                header("Location: $local");
                exit;
            }
        } 
    }
?>
