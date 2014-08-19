---
title: Emacs for Scala Keybindings
author: mnash
layout: page
---
My full Emacs setup for Scala development (and other things) is available at <a href="https://github.com/michaelpnash/emacs-for-scala" target="_new">https://github.com/michaelpnash/emacs-for-scala</a>

Below are the key bindings set up in this configuration. Click the + alongside each section to expand and view it, click again to hide that section.

<p class="trigger ">
  <a href="#toggle_125327695053f1f8e697313">Key Definitions</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          <strong>Shorthand</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>Press</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>On OSX</strong>
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x
        </td>
        
        <td align="left" valign="top">
          Control-x
        </td>
        
        <td align="left" valign="top">
          Control-x
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-x
        </td>
        
        <td align="left" valign="top">
          Meta-x
        </td>
        
        <td align="left" valign="top">
          Alt/Option-x
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          s-x
        </td>
        
        <td align="left" valign="top">
          Super-x
        </td>
        
        <td align="left" valign="top">
          Command-x
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_54870795153f1f8e6973ea">Finding Files</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          <strong>Keys</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>Description</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>Command</strong>
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x C-f
        </td>
        
        <td align="left" valign="top">
          Prompt to open file
        </td>
        
        <td align="left" valign="top">
          ido-find-file
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          &nbsp;
        </td>
        
        <td align="left" valign="top">
          Start dirtree, prompts for directory
        </td>
        
        <td align="left" valign="top">
          dirtree
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x C-M-f
        </td>
        
        <td align="left" valign="top">
          Find file in project (current dir up to the .git directory)
        </td>
        
        <td align="left" valign="top">
          find-name-dired
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          &nbsp;
        </td>
        
        <td align="left" valign="top">
          Find file by regex
        </td>
        
        <td align="left" valign="top">
          find-grep-dired
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x C-v
        </td>
        
        <td align="left" valign="top">
          Revert file to version on disk
        </td>
        
        <td align="left" valign="top">
          revert-buffer
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_134894284453f1f8e6974bf">Movement</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top" nowrap="nowrap">
          <strong>Keys</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>Description</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>Command</strong>
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-n
        </td>
        
        <td align="left" valign="top">
          Next line
        </td>
        
        <td align="left" valign="top">
          next-line
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-f
        </td>
        
        <td align="left" valign="top">
          Forward a word
        </td>
        
        <td align="left" valign="top">
          forward-word
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-b
        </td>
        
        <td align="left" valign="top">
          Backwards a word
        </td>
        
        <td align="left" valign="top">
          backward-word
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-M-b
        </td>
        
        <td align="left" valign="top">
          Go to previous open brace/comma/bracket
        </td>
        
        <td align="left" valign="top">
          backward-sexp
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-M-f
        </td>
        
        <td align="left" valign="top">
          Go to next ending brace/comma/bracket
        </td>
        
        <td align="left" valign="top">
          forward-sexp
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-M-u
        </td>
        
        <td align="left" valign="top">
          Move up in parenthesis structure
        </td>
        
        <td align="left" valign="top">
          backward-up-list
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-M-d
        </td>
        
        <td align="left" valign="top">
          Move down in parenthesis structure
        </td>
        
        <td align="left" valign="top">
          down-list
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-<
        </td>
        
        <td align="left" valign="top">
          Beginning of buffer
        </td>
        
        <td align="left" valign="top">
          beginning-of-buffer
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M->
        </td>
        
        <td align="left" valign="top">
          End of buffer
        </td>
        
        <td align="left" valign="top">
          end-of-buffer
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-m
        </td>
        
        <td align="left" valign="top">
          Back to indendation
        </td>
        
        <td align="left" valign="top">
          back-to-indentation
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          Shift-TAB
        </td>
        
        <td align="left" valign="top">
          Undent
        </td>
        
        <td align="left" valign="top">
          scala-indent:indent-with-reluctant-strategy
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-u C-x TAB
        </td>
        
        <td align="left" valign="top">
          Indent region 4 spaces
        </td>
        
        <td align="left" valign="top">
          universal-argument indent-rigidly
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-v
        </td>
        
        <td align="left" valign="top">
          Scroll up
        </td>
        
        <td align="left" valign="top">
          scroll-down-command
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-k
        </td>
        
        <td align="left" valign="top">
          Kill remainder of line
        </td>
        
        <td align="left" valign="top">
          kill-line
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          <f7>
        </td>
        
        <td align="left" valign="top">
          Kill whole line
        </td>
        
        <td align="left" valign="top">
          kill-whole-line
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-a
        </td>
        
        <td align="left" valign="top">
          Beginning of line
        </td>
        
        <td align="left" valign="top">
          move-beginning-of-line
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-e
        </td>
        
        <td align="left" valign="top">
          Ending of line
        </td>
        
        <td align="left" valign="top">
          move-end-of-line
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-v
        </td>
        
        <td align="left" valign="top">
          Scroll down
        </td>
        
        <td align="left" valign="top">
          scroll-down-command
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-l
        </td>
        
        <td align="left" valign="top">
          Goto line
        </td>
        
        <td align="left" valign="top">
          goto-line
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c SPACE
        </td>
        
        <td align="left" valign="top">
          Ace Jump to a word
        </td>
        
        <td align="left" valign="top">
          ace-jump-word-mode
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-u C-c SPACE
        </td>
        
        <td align="left" valign="top">
          Ace Jump Character Mode
        </td>
        
        <td align="left" valign="top">
          ace-jump-char-mode
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-u C-u C-c SPACE <i>OR</i> <f6>
        </td>
        
        <td align="left" valign="top">
          Ace Jump Line Mode
        </td>
        
        <td align="left" valign="top">
          ace-jump-line-mode
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-s }
        </td>
        
        <td align="left" valign="top">
          Jump to next }
        </td>
        
        <td align="left" valign="top">
          search-to-close-brace
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-S }
        </td>
        
        <td align="left" valign="top">
          Jump to previous }
        </td>
        
        <td align="left" valign="top">
          search-to-prev-close-brace
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-s {
        </td>
        
        <td align="left" valign="top">
          Jump to next {
        </td>
        
        <td align="left" valign="top">
          search-to-brace
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-S {
        </td>
        
        <td align="left" valign="top">
          Jump to previous {
        </td>
        
        <td align="left" valign="top">
          search-to-prev-brace
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-S d
        </td>
        
        <td align="left" valign="top">
          Jump to previous &#8220;def &#8220;
        </td>
        
        <td align="left" valign="top">
          search-to-next-def
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-s d
        </td>
        
        <td align="left" valign="top">
          Jump to next &#8220;def &#8220;
        </td>
        
        <td align="left" valign="top">
          search-to-next-def
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_121146410653f1f8e697590">General</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <p>
      <a name="general"></a>
    </p>
    
    <table border="1">
      <tr>
        <td align="left" valign="top" nowrap="nowrap">
          <strong>Keys</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>Description</strong>
        </td>
        
        <td align="left" valign="top">
          <strong>Command</strong>
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-s M-s
        </td>
        
        <td align="left" valign="top">
          Save all modified buffers
        </td>
        
        <td align="left" valign="top">
          save-silently
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-u 3
        </td>
        
        <td align="left" valign="top">
          Repeat next command 3 times
        </td>
        
        <td align="left" valign="top">
          universal-argument
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Prompt for input mode (tex for unicode)
        </td>
        
        <td align="left" valign="top">
          toggle-input-mode
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-t
        </td>
        
        <td align="left" valign="top">
          Transpose words
        </td>
        
        <td align="left" valign="top">
          transpose-words
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x C-t
        </td>
        
        <td align="left" valign="top">
          Transpose lines
        </td>
        
        <td align="left" valign="top">
          transpose-lines
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-t
        </td>
        
        <td align="left" valign="top">
          Transpose characters
        </td>
        
        <td align="left" valign="top">
          transpose-chars
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-M-o
        </td>
        
        <td align="left" valign="top">
          &#8220;Open&#8221; line at insertion point
        </td>
        
        <td align="left" valign="top">
          split-line
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-^
        </td>
        
        <td align="left" valign="top">
          Join the current and previous line
        </td>
        
        <td align="left" valign="top">
          delete-indentation
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x C-b
        </td>
        
        <td align="left" valign="top">
          List all buffers
        </td>
        
        <td align="left" valign="top">
          list-buffers
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x k
        </td>
        
        <td align="left" valign="top">
          Kill buffer
        </td>
        
        <td align="left" valign="top">
          ido-kill-buffer
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h c
        </td>
        
        <td align="left" valign="top">
          Show command run by given key sequence
        </td>
        
        <td align="left" valign="top">
          describe-key-briefly
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x b
        </td>
        
        <td align="left" valign="top">
          Select another buffer
        </td>
        
        <td align="left" valign="top">
          ido-switch-buffer
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-up
        </td>
        
        <td align="left" valign="top">
          Move current line or selection up
        </td>
        
        <td align="left" valign="top">
          move-text-up
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-down
        </td>
        
        <td align="left" valign="top">
          Move current line or selection down
        </td>
        
        <td align="left" valign="top">
          move-text-down
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-s
        </td>
        
        <td align="left" valign="top">
          Start an incremental search forward.
        </td>
        
        <td align="left" valign="top">
          isearch-forward
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-r
        </td>
        
        <td align="left" valign="top">
          Start an incremental search backwards
        </td>
        
        <td align="left" valign="top">
          isearch-backward
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_65882681953f1f8e697665">Ensime</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <p>
      <a href="http://ensime.github.io/" target="_new">Full Ensime Manual</a>
    </p>
    
    <table border="1" width="100%">
      <tr>
        <td align="left" valign="top" nowrap="nowrap">
          C-c C-b b
        </td>
        
        <td align="left" valign="top">
          Rebuild entire project (clean build)
        </td>
        
        <td align="left" valign="top">
          ensime-builder-build
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-b r
        </td>
        
        <td align="left" valign="top">
          Rebuild project incrementally
        </td>
        
        <td align="left" valign="top">
          ensime-builder-rebuild
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Reload the .ensime file and recompile the project
        </td>
        
        <td align="left" valign="top">
          ensime-reload
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Start the automatic configuration file generator
        </td>
        
        <td align="left" valign="top">
          ensime-config-get
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top" nowrap="nowrap">
          C-c C-v z
        </td>
        
        <td align="left" valign="top">
          Launch REPL
        </td>
        
        <td align="left" valign="top">
          ensime-inf-switch
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v i
        </td>
        
        <td align="left" valign="top">
          Launch type inspector on symbol under cursor <br /> <table border="1">
            <tr>
              <td>
                ,
              </td>
              
              <td>
                back
              </td>
            </tr>
            
            <tr>
              <td>
                .
              </td>
              
              <td>
                forward
              </td>
            </tr>
          </table>
        </td>
        
        <td align="left" valign="top">
          ensime-inspect-type-at-point
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v 5 i
        </td>
        
        <td align="left" valign="top">
          Launch type inspector on symbol under cursor in other frame
        </td>
        
        <td align="left" valign="top">
          ensime-inspect-type-at-point
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v o
        </td>
        
        <td align="left" valign="top">
          Open the inspector on the current project&#8217;s main package
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Open inspector on arbitrary type or package
        </td>
        
        <td align="left" valign="top">
          ensime-inspect-by-path
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-s
        </td>
        
        <td align="left" valign="top">
          Search through completion candidates
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-o i
        </td>
        
        <td align="left" valign="top">
          Organize imports
        </td>
        
        <td align="left" valign="top">
          ensime-refactor-organize-imports
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v v or s-o
        </td>
        
        <td align="left" valign="top">
          Search globally for methods or types
        </td>
        
        <td align="left" valign="top">
          ensime-search
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v .
        </td>
        
        <td align="left" valign="top">
          Select the surrounding syntactic context. Use . and , to grow and shrinkselection
        </td>
        
        <td align="left" valign="top">
          ensime-expand-selection-command
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-,
        </td>
        
        <td align="left" valign="top">
          Pop back to previously visited position
        </td>
        
        <td align="left" valign="top">
          ensime-pop-find-definition-stack
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-.
        </td>
        
        <td align="left" valign="top">
          Jump to definition of symbol under cursor
        </td>
        
        <td align="left" valign="top">
          ensime-edit-definition
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v i
        </td>
        
        <td align="left" valign="top">
          Inspect type under cursor<br /> <table>
            <tr>
              <td>
                .
              </td>
              
              <td>
                Forward page
              </td>
            </tr>
            
            <tr>
              <td>
                ,
              </td>
              
              <td>
                Back page
              </td>
            </tr>
            
            <tr>
              <td>
                C-n/TAB
              </td>
              
              <td>
                Forward link
              </td>
            </tr>
            
            <tr>
              <td>
                C-p
              </td>
              
              <td>
                Backward link
              </td>
            </tr>
          </table>
        </td>
        
        <td align="left" valign="top">
          &#8216;ensime-inspect-type-at-point
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          TAB
        </td>
        
        <td align="left" valign="top">
          Start completion
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v v
        </td>
        
        <td align="left" valign="top">
          Global type and method search (type uppercase for case-sensitive)
        </td>
        
        <td align="left" valign="top">
          ensime-search
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v a
        </td>
        
        <td align="left" valign="top">
          Typecheck all files in the project
        </td>
        
        <td align="left" valign="top">
          ensime-typecheck-all
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v c
        </td>
        
        <td align="left" valign="top">
          Typecheck the current file
        </td>
        
        <td align="left" valign="top">
          ensime-typecheck-current-file
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-b s
        </td>
        
        <td align="left" valign="top">
          Switch to SBT
        </td>
        
        <td align="left" valign="top">
          ensime-sbt-switch
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-b s
        </td>
        
        <td align="left" valign="top">
          SBT do compile
        </td>
        
        <td align="left" valign="top">
          ensime-sbt-do-compile
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-b n
        </td>
        
        <td align="left" valign="top">
          SBT do clean
        </td>
        
        <td align="left" valign="top">
          ensime-sbt-do-clean
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-b p
        </td>
        
        <td align="left" valign="top">
          SBT do package
        </td>
        
        <td align="left" valign="top">
          ensime-sbt-do-package
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v r
        </td>
        
        <td align="left" valign="top">
          List all references to the symbol under the cursor. Find Usages
        </td>
        
        <td align="left" valign="top">
          &#8216;ensime-show-uses-of-symbol-at-point
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v p
        </td>
        
        <td align="left" valign="top">
          Inspect the package of the current source file.
        </td>
        
        <td align="left" valign="top">
          ensime-inspect-package-at-point
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-p
        </td>
        
        <td align="left" valign="top">
          Go to the previous compilation note in the current buffer
        </td>
        
        <td align="left" valign="top">
          ensime-backward-note
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-n
        </td>
        
        <td align="left" valign="top">
          Go to the next compilation note in current buffer
        </td>
        
        <td align="left" valign="top">
          ensime-forward-note
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v u
        </td>
        
        <td align="left" valign="top">
          Undo a refactoring or formatting change
        </td>
        
        <td align="left" valign="top">
          ensime-undo-peek
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v f
        </td>
        
        <td align="left" valign="top">
          Format the current Scala file
        </td>
        
        <td align="left" valign="top">
          ensime-format-source
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v e
        </td>
        
        <td align="left" valign="top">
          Show all errors and warnings in the project
        </td>
        
        <td align="left" valign="top">
          ensime-show-all-errors-and-warnings
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-v x
        </td>
        
        <td align="left" valign="top">
          Scalex Documentation Search
        </td>
        
        <td align="left" valign="top">
          ensime-scalex
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_155990798353f1f8e697737">Ensime Refactoring</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          C-c C-r t
        </td>
        
        <td align="left" valign="top">
          Add import for type at point
        </td>
        
        <td align="left" valign="top">
          ensime-import-type-at-point
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-r r
        </td>
        
        <td align="left" valign="top">
          Rename
        </td>
        
        <td align="left" valign="top">
          ensime-refactor-rename
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-r m
        </td>
        
        <td align="left" valign="top">
          Extract method (C-space at beginning, move to end)
        </td>
        
        <td align="left" valign="top">
          ensime-refactor-extract-method
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-r i
        </td>
        
        <td align="left" valign="top">
          Inline Local
        </td>
        
        <td align="left" valign="top">
          ensime-refactor-inline-local
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-r l
        </td>
        
        <td align="left" valign="top">
          Extract local
        </td>
        
        <td align="left" valign="top">
          ensime-refactor-extract-local
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-r o
        </td>
        
        <td align="left" valign="top">
          Organize imports
        </td>
        
        <td align="left" valign="top">
          ensime-refactor-organize-imports
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_156634633553f1f8e697806">Ensime Debugger</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          C-c C-d d
        </td>
        
        <td align="left" valign="top">
          Start debugger
        </td>
        
        <td align="left" valign="top">
          ensime-db-start
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d b
        </td>
        
        <td align="left" valign="top">
          Set breakpoint
        </td>
        
        <td align="left" valign="top">
          ensime-db-set-break
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d u
        </td>
        
        <td align="left" valign="top">
          Clear breakpoint
        </td>
        
        <td align="left" valign="top">
          ensime-db-clear-break
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d s
        </td>
        
        <td align="left" valign="top">
          Step
        </td>
        
        <td align="left" valign="top">
          ensime-db-step
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d n
        </td>
        
        <td align="left" valign="top">
          Step over
        </td>
        
        <td align="left" valign="top">
          ensime-db-next
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d o
        </td>
        
        <td align="left" valign="top">
          Step out
        </td>
        
        <td align="left" valign="top">
          ensime-db-step-out
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d r
        </td>
        
        <td align="left" valign="top">
          Run
        </td>
        
        <td align="left" valign="top">
          ensime-db-run
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d c
        </td>
        
        <td align="left" valign="top">
          Continue from breakpoint
        </td>
        
        <td align="left" valign="top">
          ensime-db-continue
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d q
        </td>
        
        <td align="left" valign="top">
          Quit debug session
        </td>
        
        <td align="left" valign="top">
          ensime-db-quit
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d i
        </td>
        
        <td align="left" valign="top">
          Inspect variable at cursor in debugger
        </td>
        
        <td align="left" valign="top">
          ensime-db-inspect-value-at-point
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d t
        </td>
        
        <td align="left" valign="top">
          Show backtrace in debugger
        </td>
        
        <td align="left" valign="top">
          ensime-db-backtrace
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-d a
        </td>
        
        <td align="left" valign="top">
          Clear all breakpoints
        </td>
        
        <td align="left" valign="top">
          ensime-db-clear-all-breaks
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_91130141453f1f8e6978d4">Magit</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <p>
      <a href="http://magit.github.io/magit/magit.html" target="_new">Magit User Manual</a>
    </p>
    
    <table border="1">
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Enter magit mode, view status
        </td>
        
        <td align="left" valign="top">
          magit-status
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          S-TAB
        </td>
        
        <td align="left" valign="top">
          Toggle visibility of current section
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-S
        </td>
        
        <td align="left" valign="top">
          Show all sections
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          l l
        </td>
        
        <td align="left" valign="top">
          Show history, short form
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          l L
        </td>
        
        <td align="left" valign="top">
          Show history, more verbose form
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          s
        </td>
        
        <td align="left" valign="top">
          Move hunk into staging area
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          u
        </td>
        
        <td align="left" valign="top">
          Move hunk out of staging area (unstage)
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          S
        </td>
        
        <td align="left" valign="top">
          Move all hunks into staging
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          U
        </td>
        
        <td align="left" valign="top">
          Move all hunks out of staging
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          c
        </td>
        
        <td align="left" valign="top">
          Prompt for Commit message
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-c
        </td>
        
        <td align="left" valign="top">
          Commit
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          P P
        </td>
        
        <td align="left" valign="top">
          Push
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          F F
        </td>
        
        <td align="left" valign="top">
          Pull
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_153406473753f1f8e6979a1">Ensime Sbt Window</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          M-p
        </td>
        
        <td align="left" valign="top">
          Previously entered command
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-n
        </td>
        
        <td align="left" valign="top">
          Next entered command
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_179736096853f1f8e697a6d">Shell Commands</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          M-!
        </td>
        
        <td align="left" valign="top">
          Execute a shell command
        </td>
        
        <td align="left" valign="top">
          shell-command
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-|
        </td>
        
        <td align="left" valign="top">
          Run shell command on region
        </td>
        
        <td align="left" valign="top">
          shell-command-on-region
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-u M-|
        </td>
        
        <td align="left" valign="top">
          Filter region through shell command
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Start shell in window *shell*
        </td>
        
        <td align="left" valign="top">
          shell
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_12896647053f1f8e697b39">Org Mode</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <p>
      <a href="http://orgmode.org/org.html" target="_new">Org-Mode Full Manual</a>
    </p>
    
    <table border="1">
      <tr>
        <td align="left" valign="top">
          TAB
        </td>
        
        <td align="left" valign="top">
          Expand or contract current selection
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-c C-t
        </td>
        
        <td align="left" valign="top">
          Rotate TODO state
        </td>
        
        <td align="left" valign="top">
          org-todo
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          s-T
        </td>
        
        <td align="left" valign="top">
          Show TODO list in prio order for current file
        </td>
        
        <td align="left" valign="top">
          todo-agenda-current-file
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_16351606253f1f8e697c06">DirTree</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          s-d
        </td>
        
        <td align="left" valign="top">
          Start dirtree in it&#8217;s own buffer
        </td>
        
        <td align="left" valign="top">
          dirtree
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          D
        </td>
        
        <td align="left" valign="top">
          Delete tree
        </td>
        
        <td align="left" valign="top">
          tree-mode-delete-tree
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          p
        </td>
        
        <td align="left" valign="top">
          Previous node
        </td>
        
        <td align="left" valign="top">
          tree-mode-previous-node
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          n
        </td>
        
        <td align="left" valign="top">
          Next node
        </td>
        
        <td align="left" valign="top">
          tree-mode-next-node
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          j
        </td>
        
        <td align="left" valign="top">
          Next sibling
        </td>
        
        <td align="left" valign="top">
          tree-mode-next-sib
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          k
        </td>
        
        <td align="left" valign="top">
          Previous sibling
        </td>
        
        <td align="left" valign="top">
          tree-mode-previous-sib
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-r
        </td>
        
        <td align="left" valign="top">
          Search backwards
        </td>
        
        <td align="left" valign="top">
          tree-mode-isearch-backward
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-s
        </td>
        
        <td align="left" valign="top">
          Search forward
        </td>
        
        <td align="left" valign="top">
          tree-mode-isearch-forward
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          !
        </td>
        
        <td align="left" valign="top">
          Collapse other except
        </td>
        
        <td align="left" valign="top">
          tree-mode-collaps-other-except
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          /
        </td>
        
        <td align="left" valign="top">
          Keep match
        </td>
        
        <td align="left" valign="top">
          tree-mode-keep-match
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Start dirtree in this buffer
        </td>
        
        <td align="left" valign="top">
          dirtree-in-buffer
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          s
        </td>
        
        <td align="left" valign="top">
          Sort by tag
        </td>
        
        <td align="left" valign="top">
          tree-mode-sort-by-tag
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          e
        </td>
        
        <td align="left" valign="top">
          Toggle expand
        </td>
        
        <td align="left" valign="top">
          tree-mode-toggle-expand
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          E
        </td>
        
        <td align="left" valign="top">
          Expand level
        </td>
        
        <td align="left" valign="top">
          tree-mode-expand-level
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          g
        </td>
        
        <td align="left" valign="top">
          Reflesh tree
        </td>
        
        <td align="left" valign="top">
          tree-mode-reflesh
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          r
        </td>
        
        <td align="left" valign="top">
          Goto root
        </td>
        
        <td align="left" valign="top">
          tree-mode-goto-root
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          u
        </td>
        
        <td align="left" valign="top">
          Goto parent
        </td>
        
        <td align="left" valign="top">
          tree-mode-got-parent
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_132846890953f1f8e697cda">Table Mode</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <p>
      <a href="http://table.sourceforge.net/" target="_new">Sourceforge Page for Table Mode</a>
    </p>
    
    <table border="1">
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Insert new table
        </td>
        
        <td align="left" valign="top">
          table-insert
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-+
        </td>
        
        <td align="left" valign="top">
          Insert row
        </td>
        
        <td align="left" valign="top">
          table-insert-row
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-+
        </td>
        
        <td align="left" valign="top">
          Insert column
        </td>
        
        <td align="left" valign="top">
          table-insert-column
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Delete row
        </td>
        
        <td align="left" valign="top">
          table-delete-row
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Delete column
        </td>
        
        <td align="left" valign="top">
          table-delete-column
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Recognize all table in current buffer
        </td>
        
        <td align="left" valign="top">
          table-recognize
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Unrecognize tables in current buffer
        </td>
        
        <td align="left" valign="top">
          table-unrecognize
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Recognize in region
        </td>
        
        <td align="left" valign="top">
          table-recognize-region
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Unrecognize in region
        </td>
        
        <td align="left" valign="top">
          table-unrecognize-region
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Recognize single table
        </td>
        
        <td align="left" valign="top">
          table-recognize-table
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Unrecognize single table
        </td>
        
        <td align="left" valign="top">
          table-unrecognize-table
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Recognize a cell at current point
        </td>
        
        <td align="left" valign="top">
          table-recognize-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Unrecognize cell at point
        </td>
        
        <td align="left" valign="top">
          table-unrecognize-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Move forward to next Nth cell
        </td>
        
        <td align="left" valign="top">
          table-forward-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Move previous Nth cell
        </td>
        
        <td align="left" valign="top">
          table-backward-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-*
        </td>
        
        <td align="left" valign="top">
          Span current cell in specified direction
        </td>
        
        <td align="left" valign="top">
          table-span-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C&#8211;
        </td>
        
        <td align="left" valign="top">
          Split current cell vertically
        </td>
        
        <td align="left" valign="top">
          table-split-cell-vertically
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-|
        </td>
        
        <td align="left" valign="top">
          Split current cell horizontally
        </td>
        
        <td align="left" valign="top">
          table-split-cell-horizontally
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Split current cell vertically or horizontally
        </td>
        
        <td align="left" valign="top">
          table-split-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-}
        </td>
        
        <td align="left" valign="top">
          Increase height of current cell
        </td>
        
        <td align="left" valign="top">
          table-heighten-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-{
        </td>
        
        <td align="left" valign="top">
          Decrease height of current cell
        </td>
        
        <td align="left" valign="top">
          table-shorten-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-<
        </td>
        
        <td align="left" valign="top">
          Narrow current cell
        </td>
        
        <td align="left" valign="top">
          table-narrow-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C->
        </td>
        
        <td align="left" valign="top">
          Widen current cell
        </td>
        
        <td align="left" valign="top">
          table-widen-cell
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-!
        </td>
        
        <td align="left" valign="top">
          Toggle fixed width mode
        </td>
        
        <td align="left" valign="top">
          table-fixed-width-mode
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-#
        </td>
        
        <td align="left" valign="top">
          Compute and report current table dimension
        </td>
        
        <td align="left" valign="top">
          table-query-dimension
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-^
        </td>
        
        <td align="left" valign="top">
          Generate source in specified language andinsert into specified buffer
        </td>
        
        <td align="left" valign="top">
          table-generate-source
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Travel forward inserting specified sequencein cells
        </td>
        
        <td align="left" valign="top">
          table-insert-sequence
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Convert plant text into table by capturingtext in the region
        </td>
        
        <td align="left" valign="top">
          table-capture
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Convert table into plain text
        </td>
        
        <td align="left" valign="top">
          table-release
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-:
        </td>
        
        <td align="left" valign="top">
          Justify contents of cells
        </td>
        
        <td align="left" valign="top">
          table-justify
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Disable all table advice
        </td>
        
        <td align="left" valign="top">
          table-disable-advice
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Enable table advice
        </td>
        
        <td align="left" valign="top">
          table-enable-advice
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Show version of table mode
        </td>
        
        <td align="left" valign="top">
          table-version
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          TAB
        </td>
        
        <td align="left" valign="top">
          Move point to beginning of next cell
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_166401666553f1f8e697daf">Window Commands</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          C-x 2
        </td>
        
        <td align="left" valign="top">
          Divide the current window horizontally in two
        </td>
        
        <td align="left" valign="top">
          split-window-horizontally
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x 5
        </td>
        
        <td align="left" valign="top">
          Divide the current window vertically in two.
        </td>
        
        <td align="left" valign="top">
          split-windws-vertically
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x >
        </td>
        
        <td align="left" valign="top">
          Scroll the window right.
        </td>
        
        <td align="left" valign="top">
          scroll-right
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x <
        </td>
        
        <td align="left" valign="top">
          Scroll the window left.
        </td>
        
        <td align="left" valign="top">
          scroll-left
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x 0
        </td>
        
        <td align="left" valign="top">
          Delete the current window.
        </td>
        
        <td align="left" valign="top">
          delete-window
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x 1
        </td>
        
        <td align="left" valign="top">
          Delete all the windows except this one.
        </td>
        
        <td align="left" valign="top">
          delete-other-windows
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Delete all windows open to a particular buff.
        </td>
        
        <td align="left" valign="top">
          delete-windows-on
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x ^
        </td>
        
        <td align="left" valign="top">
          Make the current window taller.
        </td>
        
        <td align="left" valign="top">
          enlarge-window
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Make the current window smaller.
        </td>
        
        <td align="left" valign="top">
          shrink-window
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x }
        </td>
        
        <td align="left" valign="top">
          Make the window wider.
        </td>
        
        <td align="left" valign="top">
          enlarge-window-horizontally
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x {
        </td>
        
        <td align="left" valign="top">
          Make the window less wide.
        </td>
        
        <td align="left" valign="top">
          shrink-window-horizontally
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-C-v
        </td>
        
        <td align="left" valign="top">
          Scroll the other window.
        </td>
        
        <td align="left" valign="top">
          scroll-other-window
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x 4 f
        </td>
        
        <td align="left" valign="top">
          Find a file in the other window.
        </td>
        
        <td align="left" valign="top">
          find-file-other-window
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x 4 b
        </td>
        
        <td align="left" valign="top">
          Select a buffer in the other window.
        </td>
        
        <td align="left" valign="top">
          switch-to-buffer-other-window
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          Compare two buffers and show the first diff.
        </td>
        
        <td align="left" valign="top">
          compare-windows
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_174292440053f1f8e697e7d">Capitalization</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          M-c
        </td>
        
        <td align="left" valign="top">
          Capitalize the first letter of current word.
        </td>
        
        <td align="left" valign="top">
          capitalize-word
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-u
        </td>
        
        <td align="left" valign="top">
          Make the word all uppercase.
        </td>
        
        <td align="left" valign="top">
          upcase-word
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M-l
        </td>
        
        <td align="left" valign="top">
          Make the word all lowercase.
        </td>
        
        <td align="left" valign="top">
          downcase-word
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x C-l
        </td>
        
        <td align="left" valign="top">
          Make the region all lowercase.
        </td>
        
        <td align="left" valign="top">
          downcase-region
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-x C-u
        </td>
        
        <td align="left" valign="top">
          Make the region all uppercase.
        </td>
        
        <td align="left" valign="top">
          uppercase-region
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_45759399353f1f8e697f77">Getting Help</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table border="1">
      <tr>
        <td align="left" valign="top">
          C-h a
        </td>
        
        <td align="left" valign="top">
          What commands work like this&#8230;?
        </td>
        
        <td align="left" valign="top">
          command-apropos
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
        </td>
        
        <td align="left" valign="top">
          What functions and variables work like this.?
        </td>
        
        <td align="left" valign="top">
          apropos
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h c
        </td>
        
        <td align="left" valign="top">
          What command does this key sequence do?
        </td>
        
        <td align="left" valign="top">
          describe-key-briefly
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h b
        </td>
        
        <td align="left" valign="top">
          What are the key bindings for this buffer?
        </td>
        
        <td align="left" valign="top">
          describe-bindings
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h k
        </td>
        
        <td align="left" valign="top">
          What command does this sequence do,and tell me about it.
        </td>
        
        <td align="left" valign="top">
          describe-key
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h l
        </td>
        
        <td align="left" valign="top">
          What are the last 100 characters typed?
        </td>
        
        <td align="left" valign="top">
          view-lossage
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h w
        </td>
        
        <td align="left" valign="top">
          What is the key binding for this?
        </td>
        
        <td align="left" valign="top">
          where-is
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h f
        </td>
        
        <td align="left" valign="top">
          What does this function do?
        </td>
        
        <td align="left" valign="top">
          describe-function
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h v
        </td>
        
        <td align="left" valign="top">
          What is this variable?
        </td>
        
        <td align="left" valign="top">
          describe-variable
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h m
        </td>
        
        <td align="left" valign="top">
          Tell me about this mode.
        </td>
        
        <td align="left" valign="top">
          describe-mode
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-h s
        </td>
        
        <td align="left" valign="top">
          What is the syntax table for this buffer?
        </td>
        
        <td align="left" valign="top">
          describe-syntax
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_108693708453f1f8e698065">Tmux</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <p>
      <a href="http://tmux.sourceforge.net/" target="_new">Tmux Sourceforge Page</a>
    </p>
    
    <table border="1">
      <tr>
        <td align="left" valign="top">
          Keys
        </td>
        
        <td align="left" valign="top">
          Description
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-b d
        </td>
        
        <td align="left" valign="top">
          Detach Session
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          C-b ?
        </td>
        
        <td align="left" valign="top">
          Show Keybindings
        </td>
      </tr>
    </table>
    
    <table border="1">
      <tr>
        <td align="left" valign="top">
          tmux -S /tmp/xyz
        </td>
        
        <td align="left" valign="top">
          Start session in file /tmp/xyz (must chmod to 777 to share)
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          tmux -S /tmp/xyz attach
        </td>
        
        <td align="left" valign="top">
          Attach to an existing session in /tmp/xyz
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_38825162153f1f8e69813e">Dired</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <p>
      <a href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html#Dired" target="_new">Dired Manual</a>
    </p>
    
    <p>
      Perform query-replace-regexp on each of the specified files, replacing matches for regexp with the string todired-do-query-replace-regexptToggle all marks in current directory
    </p>
    
    <table>
      <tr>
        <td>
          C-x d
        </td>
        
        <td>
          Start dired in a specified directory (prompts for directory)
        </td>
        
        <td>
          dired
        </td>
      </tr>
      
      <tr>
        <td>
          C-n
        </td>
        
        <td>
          Next node
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          <space>
        </td>
        
        <td>
          Next node
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          n
        </td>
        
        <td>
          Next node
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          C-p
        </td>
        
        <td>
          Previous node
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          <del>
        </td>
        
        <td>
          Move up and unflag
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          j
        </td>
        
        <td>
          Prompt for filename, move to the line with that file name
        </td>
        
        <td>
          dired-goto-file
        </td>
      </tr>
      
      <tr>
        <td>
          i
        </td>
        
        <td>
          Insert contents of directory at point
        </td>
        
        <td>
          dired-maybe-insert-subdir
        </td>
      </tr>
      
      <tr>
        <td>
          l
        </td>
        
        <td>
          Refresh directory contents
        </td>
        
        <td>
          dired-do-redisplay
        </td>
      </tr>
      
      <tr>
        <td>
          ^
        </td>
        
        <td>
          Move point to parent directory entry
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          $
        </td>
        
        <td>
          Hide/Unhide subdirectory, leaving only header line visible
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          M-$
        </td>
        
        <td>
          Hide/Unhide all subdirectories, leaving only header lines visible
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          C-M-n
        </td>
        
        <td>
          Go to next subdirectory header line, regardless of level
        </td>
        
        <td>
          dired-next-subdir
        </td>
      </tr>
      
      <tr>
        <td>
          C-M-p
        </td>
        
        <td>
          Go to previous subdirectory header line, regardless of level
        </td>
        
        <td>
          dired-prev-subdir
        </td>
      </tr>
      
      <tr>
        <td>
          C-M-u
        </td>
        
        <td>
          Go up to the parent directory&#8217;s header line
        </td>
        
        <td>
          dired-tree-up
        </td>
      </tr>
      
      <tr>
        <td>
          C-M-d
        </td>
        
        <td>
          Go down in the directory tree, to the first subdirectory&#8217;s header line
        </td>
        
        <td>
          dired-tree-down
        </td>
      </tr>
      
      <tr>
        <td>
          M-x image-dired
        </td>
        
        <td>
          Enter image-dired mode, show thumbnails of images in this directory
        </td>
      </tr>
      
      <tr>
        <td>
          C-t d
        </td>
        
        <td>
          Display thumbnails of marked images in this diredtory
        </td>
        
        <td>
          image-dired-display-thumbs
        </td>
      </tr>
      
      <tr>
        <td>
          <
        </td>
        
        <td>
          Move up to the previous directory-file line
        </td>
        
        <td>
          dired-prev-dirline
        </td>
      </tr>
      
      <tr>
        <td>
          >
        </td>
        
        <td>
          Move down to the next directory-file line
        </td>
        
        <td>
          dired-prev-dirline
        </td>
      </tr>
      
      <tr>
        <td>
          C-x C-q
        </td>
        
        <td>
          Toggle WDired mode, <a href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Wdired.html#Wdired" target="_new">see this manual for details</a>
        </td>
        
        <td>
          dired-toggle-read-only
        </td>
      </tr>
      
      <tr>
        <td>
          d
        </td>
        
        <td>
          Flag this file for deletion
        </td>
        
        <td>
          dired-flag-file-deletion
        </td>
      </tr>
      
      <tr>
        <td>
          u
        </td>
        
        <td>
          Remove the deletion flag
        </td>
        
        <td>
          dired-unmark
        </td>
      </tr>
      
      <tr>
        <td>
          <DEL>
        </td>
        
        <td>
          Move point to previous line and remove the deletion flag on that line
        </td>
        
        <td>
          dired-unmark-backward
        </td>
      </tr>
      
      <tr>
        <td>
          x
        </td>
        
        <td>
          Delete files flagged for deletion
        </td>
        
        <td>
          dired-do-flagged-delete
        </td>
      </tr>
      
      <tr>
        <td>
          * % regexp <RET>
        </td>
        
        <td>
          Mark with a &#8216;*&#8217; all files whose name matches the specified regexp
        </td>
        
        <td>
          dired-mark-files-regexp
        </td>
      </tr>
      
      <tr>
        <td>
          % g regexp <RET>
        </td>
        
        <td>
          Mark with a &#8216;*&#8217; all files whose <i>contents</i> match the specified regexp
        </td>
        
        <td>
          dired-mark-files-containing-regexp
        </td>
      </tr>
      
      <tr>
        <td>
          C-/
        </td>
        
        <td>
          Undo changes in the dired buffer
        </td>
        
        <td>
          dired-undo
        </td>
      </tr>
      
      <tr>
        <td>
          C
        </td>
        
        <td>
          Copy File
        </td>
        
        <td>
          dired-do-copy
        </td>
      </tr>
      
      <tr>
        <td>
          s-j
        </td>
        
        <td>
          Jump to dired of directory containing the current file
        </td>
        
        <td>
          dired-jump
        </td>
      </tr>
      
      <tr>
        <td>
          D
        </td>
        
        <td>
          Delete file
        </td>
        
        <td>
          dired-do-delete
        </td>
      </tr>
      
      <tr>
        <td>
          R
        </td>
        
        <td>
          Rename file
        </td>
        
        <td>
          dired-do-rename
        </td>
      </tr>
      
      <tr>
        <td>
          M
        </td>
        
        <td>
          Change mode of file
        </td>
        
        <td>
          dired-do-chmod
        </td>
      </tr>
      
      <tr>
        <td>
          A regexp <RET>
        </td>
        
        <td>
          Search all the specified files for the regular expression regexp
        </td>
        
        <td>
          dired-do-search
        </td>
      </tr>
      
      <tr>
        <td>
          Q regexp <RET> to <RET>
        </td>
      </tr>
      
      <tr>
        <td>
          m
        </td>
        
        <td>
          Mark current file/directory
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          u
        </td>
        
        <td>
          Unmark current file/directory
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          U
        </td>
        
        <td>
          Unmark all marked in current directory
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          M&#8211;
        </td>
        
        <td align="left" valign="top">
          Toggle Tree View
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
      
      <tr>
        <td align="left" valign="top">
          m
        </td>
        
        <td align="left" valign="top">
          Mark one file
        </td>
        
        <td align="left" valign="top">
        </td>
      </tr>
    </table>
    
    <p>
      <a href="http://www.emacswiki.org/emacs/dired-details.el" target="_new">Dired Details on EmacsWiki</a>
    </p>
    
    <table>
      <tr>
        <td>
          )
        </td>
        
        <td>
          Show more details on each file/dir
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          (
        </td>
        
        <td>
          Show less details on each file/dir
        </td>
        
        <td>
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>

<p class="trigger ">
  <a href="#toggle_86341151153f1f8e698213">Multiple Cursors</a>
</p>

<div class="toggle_container" style="display:none;">
  <div class="block">
    <table>
      <tr>
        <td>
          C-S-c C-S-c
        </td>
        
        <td>
          Multiple cursors on lines in active region
        </td>
        
        <td>
          mc/edit-lines
        </td>
      </tr>
      
      <tr>
        <td>
          C->
        </td>
        
        <td>
          Mark next line like this
        </td>
        
        <td>
          mc/mark-next-like-this
        </td>
      </tr>
      
      <tr>
        <td>
          C-<
        </td>
        
        <td>
          Mark previous line like this
        </td>
        
        <td>
          mc/mark-previous-like-this
        </td>
      </tr>
      
      <tr>
        <td>
          C-c C-<
        </td>
        
        <td>
          Mark all like this (select a region to match first)
        </td>
        
        <td>
          mc/mark-all-like-this
        </td>
      </tr>
      
      <tr>
        <td>
          C-g
        </td>
        
        <td>
          Cancel multiple cursor mode
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          RET
        </td>
        
        <td>
          Exit multiple cursor mode
        </td>
        
        <td>
        </td>
      </tr>
      
      <tr>
        <td>
          C-j
        </td>
        
        <td>
          Insert a newline in multiple-cursor mode
        </td>
        
        <td>
        </td>
      </tr>
    </table>
  </div></p>
</div>

<div class="clear">
</div>