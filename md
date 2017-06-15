#!/usr/bin/php
<?php

require __DIR__ . '/vendor/autoload.php';

use cebe\markdown\GithubMarkdown;

$parser = new GithubMarkdown();

array_shift($argv);

if (!empty($argv)) {
    $template = file_get_contents(__DIR__ . '/markdown-template.html');
    $markdown_css = file_get_contents(__DIR__ . '/node_modules/github-markdown-css/github-markdown.css');

    $template = str_replace('/* markdown_css */', $markdown_css, $template);

    foreach ($argv as $file) {
        $markdown = file_get_contents($file);

        if ($markdown) {
            $html = $parser->parse($markdown);
            $html = str_replace('<!-- markdown_body -->', $html, $template);
            
            if ($html) {
                $tempname = tempnam(sys_get_temp_dir(), 'markdown');
                
                rename($tempname, $tempname . '.html');
                
                $tempname .= '.html';

                file_put_contents($tempname, $html);
                
                passthru('open ' . $tempname);
            }
        }
    }
} else {
    echo "Provide one or more file names as arguments\n";
}