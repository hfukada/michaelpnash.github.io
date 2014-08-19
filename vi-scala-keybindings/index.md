---
title: Vi for Scala Keybindings
author: mnash
layout: page
---
Key bindings for my Vi setup for editing Scala, [available here][1].

<div style="text-align: center;">
  <span style="font-weight: bold;">Vi</span>
</div>

<table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
  <tr>
    <td style="vertical-align: top;">
      <div>
      </div>
      
      <div style="text-align: center;">
        <span style="font-weight: bold;">Buffers</span>
      </div>
      
      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
        <tr>
          <td style="vertical-align: top;">
            ,b
          </td>
          
          <td style="vertical-align: top; text-align: left;">
            Next Buffer
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,B
          </td>
          
          <td style="vertical-align: top;">
            Previous Buffer
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            :buffers
          </td>
          
          <td style="vertical-align: top;">
            List all current buffers
          </td>
        </tr>
      </table>
      
      <div style="text-align: center;">
        <span style="font-weight: bold;">Folding</span>
      </div>
      
      <table width="100%" border="1">
        <tr>
          <td>
            za
          </td>
          
          <td>
            Toggle current fold, current level
          </td>
        </tr>
        
        <tr>
          <td>
            zo
          </td>
          
          <td>
            Open fold, current level
          </td>
        </tr>
        
        <tr>
          <td>
            zc
          </td>
          
          <td>
            Close fold, current level
          </td>
        </tr>
        
        <tr>
          <td>
            zA
          </td>
          
          <td>
            Toggle current fold, all levels
          </td>
        </tr>
        
        <tr>
          <td>
            zo
          </td>
          
          <td>
            Open fold, all levels
          </td>
        </tr>
        
        <tr>
          <td>
            zc
          </td>
          
          <td>
            Close fold, all levels
          </td>
        </tr>
        
        <tr>
          <td>
            zr
          </td>
          
          <td>
            Open one more level of folds, whole buffer
          </td>
        </tr>
        
        <tr>
          <td>
            zR
          </td>
          
          <td>
            Open all folds, whole buffer
          </td>
        </tr>
        
        <tr>
          <td>
            zm
          </td>
          
          <td>
            Close one more level of folds, whole buffer
          </td>
        </tr>
        
        <tr>
          <td>
            zM
          </td>
          
          <td>
            Close all folds, whole buffer
          </td>
        </tr>
      </table>
      
      <div style="text-align: center;">
        <span style="font-weight: bold;">Visual Block Mode</span>
      </div>
      
      <table width="100%" border="1">
        <tr>
          <td>
            v
          </td>
          
          <td>
            Enter block mode
          </td>
        </tr>
        
        <tr>
          <td>
            I
          </td>
          
          <td>
            Insert into block at current cursor position
          </td>
        </tr>
        
        <tr>
          <td>
            h
          </td>
          
          <td>
            Move block end to the left
          </td>
        </tr>
        
        <tr>
          <td>
            j
          </td>
          
          <td>
            Move block end down
          </td>
        </tr>
        
        <tr>
          <td>
            k
          </td>
          
          <td>
            Move block end up
          </td>
        </tr>
        
        <tr>
          <td>
            l
          </td>
          
          <td>
            Move block end right
          </td>
        </tr>
        
        <tr>
          <td>
            x
          </td>
          
          <td>
            Delete block
          </td>
        </tr>
        
        <tr>
          <td>
            <SPACE>
          </td>
          
          <td>
            Same as l, move block end right
          </td>
        </tr>
        
        <tr>
          <td>
            A
          </td>
          
          <td>
            Append to block at current position
          </td>
        </tr>
      </table>
    </td>
    
    <td style="vertical-align: top;">
      <div style="text-align: center;">
        <span style="font-weight: bold;">Movement</span>
      </div>
      
      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
        <tr>
          <td style="vertical-align: top;">
            j
          </td>
          
          <td style="vertical-align: top;">
            Move one line down
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            k
          </td>
          
          <td style="vertical-align: top;">
            Move one line up
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            l
          </td>
          
          <td style="vertical-align: top;">
            Move one character right
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            h
          </td>
          
          <td style="vertical-align: top;">
            Move one character left
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            {
          </td>
          
          <td style="vertical-align: top;">
            Jump to previous blank line
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            }
          </td>
          
          <td style="vertical-align: top;">
            Jump to next blank line
          </td>
        </tr>
      </table>
      
      <div style="text-align: center;">
        <span style="font-weight: bold;">Windows</span>
      </div>
      
      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
        <tr>
          <td style="vertical-align: top;">
            :split
          </td>
          
          <td style="vertical-align: top;">
            Split window
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,sw
          </td>
          
          <td style="vertical-align: top;">
            Size current window to fit<br /> lines in file (for small files)
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            :resize 10
          </td>
          
          <td style="vertical-align: top;">
            Size current (horiz) window to 10 lines
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            :vertical resize 10
          </td>
          
          <td style="vertical-align: top;">
            Size current (vertical) window to 10 columns
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            C-w=
          </td>
          
          <td style="vertical-align: top;">
            Make all windows the same size
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            C-w-
          </td>
          
          <td style="vertical-align: top;">
            Make current horizontal-split window smaller by one line (can prefix with number)
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            C-w+
          </td>
          
          <td style="vertical-align: top;">
            Make current horizontal-split window larger by one line (can prefix with number)
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            C-w<
          </td>
          
          <td style="vertical-align: top;">
            Make current window narrower by one column (can prefix with number)
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            C-w>
          </td>
          
          <td style="vertical-align: top;">
            Make vertical split window wider by one column (can prefix with number)
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            :new XXX
          </td>
          
          <td style="vertical-align: top;">
            Open file xxx in new window. Prefix with number to set size of window
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,t
          </td>
          
          <td style="vertical-align: top;">
            Open corresponding Test file in a split <span style="font-style: italic;">below</span> this window
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,T
          </td>
          
          <td style="vertical-align: top;">
            Open corresponding Test file in this window (new buffer)
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,vt
          </td>
          
          <td style="vertical-align: top;">
            Open corresponding Test file in a split to the <span style="font-style: italic;">right</span> of this window
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,at
          </td>
          
          <td style="vertical-align: top;">
            Open corresponding Test file in a split <span style="font-style: italic;">above</span> this window
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,lt
          </td>
          
          <td style="vertical-align: top;">
            Open corresponding Test file in a split to the <span style="font-style: italic;">left</span> of this window
          </td>
        </tr>
      </table>
      
      <div style="text-align: center;">
        <span style="font-weight: bold;">Comments</span>
      </div>
      
      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
        <tr>
          <td style="vertical-align: top;">
            ,cc
          </td>
          
          <td style="vertical-align: top;">
            Comment-out marked region
          </td>
        </tr>
        
        <tr>
          <td style="vertical-align: top;">
            ,cu
          </td>
          
          <td style="vertical-align: top;">
            Remove comments from marked region
          </td>
        </tr>
      </table>
      
      <p>
        &nbsp;</td> </tr> <tr>
          <td style="vertical-align: top;">
            <div style="text-align: center;">
              <span style="font-weight: bold;">QuickFix</span>
            </div>
            
            <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
              <tr>
                <td style="vertical-align: top;">
                  \ff
                </td>
                
                <td style="vertical-align: top;">
                  Jump to first compile error
                </td>
              </tr>
              
              <tr>
                <td style="vertical-align: top;">
                  \fn
                </td>
                
                <td style="vertical-align: top;">
                  Jump to next compile error
                </td>
              </tr>
              
              <tr>
                <td style="vertical-align: top;">
                  :cope [n]
                </td>
                
                <td style="vertical-align: top;">
                  Open window with list of errors. n is optional window height
                </td>
              </tr>
              
              <tr>
                <td style="vertical-align: top;">
                  :ccl
                </td>
                
                <td style="vertical-align: top;">
                  Close list of errors
                </td>
              </tr>
            </table>
            
            <p>
              &nbsp;</td> <td style="vertical-align: top;">
                <div style="text-align: center;">
                  <span style="font-weight: bold;">Tags</span>
                </div>
                
                <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                  <tr>
                    <td style="vertical-align: top;">
                      :tag XXX
                    </td>
                    
                    <td style="vertical-align: top;">
                      Jump to definition of symbol XXX
                    </td>
                  </tr>
                  
                  <tr>
                    <td style="vertical-align: top;">
                      C-]
                    </td>
                    
                    <td style="vertical-align: top;">
                      Jump to definition of tag under cursor
                    </td>
                  </tr>
                  
                  <tr>
                    <td style="vertical-align: top;">
                      C-t
                    </td>
                    
                    <td style="vertical-align: top;">
                      Jump back to point before jumping to definition
                    </td>
                  </tr>
                </table>
                
                <p>
                  &nbsp;</td> </tr> <tr>
                    <td style="vertical-align: top;">
                      <div style="text-align: center;">
                        <span style="font-weight: bold;">NERDTree</span>
                      </div>
                      
                      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                        <tr>
                          <td style="vertical-align: top;">
                            C-n
                          </td>
                          
                          <td style="vertical-align: top;">
                            Toggle NERDTree window
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            r
                          </td>
                          
                          <td style="vertical-align: top;">
                            Refresh current dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            R
                          </td>
                          
                          <td style="vertical-align: top;">
                            Refresh from root dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            P
                          </td>
                          
                          <td style="vertical-align: top;">
                            Jump to root node
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            o/RETURN
                          </td>
                          
                          <td style="vertical-align: top;">
                            Open file, dir or bookmark
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            go
                          </td>
                          
                          <td style="vertical-align: top;">
                            Open, but cursor stays in tree
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            t
                          </td>
                          
                          <td style="vertical-align: top;">
                            Open in new tab
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            T
                          </td>
                          
                          <td style="vertical-align: top;">
                            Like t, but focus stays on current tab
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            i
                          </td>
                          
                          <td style="vertical-align: top;">
                            Open in split window
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            gi
                          </td>
                          
                          <td style="vertical-align: top;">
                            Same as i, but cursor stays in tree
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            s
                          </td>
                          
                          <td style="vertical-align: top;">
                            Open in vsplit
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            gs
                          </td>
                          
                          <td style="vertical-align: top;">
                            Same as s, but cursor stays in tree
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            O
                          </td>
                          
                          <td style="vertical-align: top;">
                            Recursively open selected dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            x
                          </td>
                          
                          <td style="vertical-align: top;">
                            Close current nodes parent
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            X
                          </td>
                          
                          <td style="vertical-align: top;">
                            Recursively close all children of current node
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            e
                          </td>
                          
                          <td style="vertical-align: top;">
                            Edit current dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            D
                          </td>
                          
                          <td style="vertical-align: top;">
                            Delete current bookmark
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            p
                          </td>
                          
                          <td style="vertical-align: top;">
                            Jump to current roots parent
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            K
                          </td>
                          
                          <td style="vertical-align: top;">
                            Jump up inside dirs at current depth
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            J
                          </td>
                          
                          <td style="vertical-align: top;">
                            Jump down inside dirs at current depth
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-J
                          </td>
                          
                          <td style="vertical-align: top;">
                            Jump down to next sibling of current dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-K
                          </td>
                          
                          <td style="vertical-align: top;">
                            Jump up to prev sibling of current dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C
                          </td>
                          
                          <td style="vertical-align: top;">
                            Change root to selected dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            u
                          </td>
                          
                          <td style="vertical-align: top;">
                            Move tree root up one dir
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            U
                          </td>
                          
                          <td style="vertical-align: top;">
                            Same as u, but old root left open
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            m
                          </td>
                          
                          <td style="vertical-align: top;">
                            Display action menu
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            cd
                          </td>
                          
                          <td style="vertical-align: top;">
                            Change cwd to dir of selected node
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            CD
                          </td>
                          
                          <td style="vertical-align: top;">
                            Change root to dir of current node
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            I
                          </td>
                          
                          <td style="vertical-align: top;">
                            Toggle hidden files
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            f
                          </td>
                          
                          <td style="vertical-align: top;">
                            Toggle file filters
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            F
                          </td>
                          
                          <td style="vertical-align: top;">
                            Toggle display of files
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            B
                          </td>
                          
                          <td style="vertical-align: top;">
                            Toogle bookmark table
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            q
                          </td>
                          
                          <td style="vertical-align: top;">
                            Close NERDTree window
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            A
                          </td>
                          
                          <td style="vertical-align: top;">
                            Maximize NERDTree window
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            ?
                          </td>
                          
                          <td style="vertical-align: top;">
                            Quick help
                          </td>
                        </tr>
                      </table>
                      
                      <div style="text-align: center;">
                        <span style="font-weight: bold;">Marks</span>
                      </div>
                      
                      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                        <tr>
                          <td style="vertical-align: top;">
                            mx
                          </td>
                          
                          <td style="vertical-align: top;">
                            Set mark &#8220;x&#8221; (where x is any lower-case letter)
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            &#8216;x
                          </td>
                          
                          <td style="vertical-align: top;">
                            Go to beginning of line of mark x
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            `x
                          </td>
                          
                          <td style="vertical-align: top;">
                            Go to exact position of mark x
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            mX
                          </td>
                          
                          <td style="vertical-align: top;">
                            Create mark on this file called X (uppercase letter)
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            `X
                          </td>
                          
                          <td style="vertical-align: top;">
                            Go to file marked X (uppercase)
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            &#8216;X
                          </td>
                          
                          <td style="vertical-align: top;">
                            Same as `X
                          </td>
                        </tr>
                      </table>
                      
                      <div style="text-align: center;">
                        <span style="font-weight: bold;">Special Marks</span>
                      </div>
                      
                      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                        <tr>
                          <td style="vertical-align: top;">
                            &#8216;
                          </td>
                          
                          <td style="vertical-align: top;">
                            Last position before a jump
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            <
                          </td>
                          
                          <td style="vertical-align: top;">
                            Start of visual
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            >
                          </td>
                          
                          <td style="vertical-align: top;">
                            End of visual
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            [
                          </td>
                          
                          <td style="vertical-align: top;">
                            Start of previously changed text
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            ]
                          </td>
                          
                          <td style="vertical-align: top;">
                            End of previously changed text
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            ^
                          </td>
                          
                          <td style="vertical-align: top;">
                            Last insert
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            .
                          </td>
                          
                          <td style="vertical-align: top;">
                            Last change
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            (
                          </td>
                          
                          <td style="vertical-align: top;">
                            Start of sentence
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            )
                          </td>
                          
                          <td style="vertical-align: top;">
                            End of sentence
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            {
                          </td>
                          
                          <td style="vertical-align: top;">
                            Start of paragraph
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            }
                          </td>
                          
                          <td style="vertical-align: top;">
                            End of paragraph
                          </td>
                        </tr>
                      </table>
                    </td>
                    
                    <td style="vertical-align: top;">
                      <div style="text-align: center;">
                        <span style="font-weight: bold;">Control-P</span>
                      </div>
                      
                      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                        <tr>
                          <td style="vertical-align: top;">
                            C-p
                          </td>
                          
                          <td style="vertical-align: top;">
                            Invoke in file mode
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-P
                          </td>
                          
                          <td style="vertical-align: top;">
                            Invoke in mixed mode (files, buffers, MRU)
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            <f5>
                          </td>
                          
                          <td style="vertical-align: top;">
                            Purge cache
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-f/C-n
                          </td>
                          
                          <td style="vertical-align: top;">
                            Cycle through modes
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-d
                          </td>
                          
                          <td style="vertical-align: top;">
                            Filename-only mode (instead of full path)
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-r
                          </td>
                          
                          <td style="vertical-align: top;">
                            Regex mode
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-j/C-k
                          </td>
                          
                          <td style="vertical-align: top;">
                            Navigate result list
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-t/C-v/C-x
                          </td>
                          
                          <td style="vertical-align: top;">
                            Open selected entry in new tab or new split
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-n/C-p
                          </td>
                          
                          <td style="vertical-align: top;">
                            Next/Prev prompt history
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-y
                          </td>
                          
                          <td style="vertical-align: top;">
                            Create new file and parent dirs
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-z
                          </td>
                          
                          <td style="vertical-align: top;">
                            Mark/Unmark multiple files
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            C-o
                          </td>
                          
                          <td style="vertical-align: top;">
                            Open marked files
                          </td>
                        </tr>
                      </table>
                      
                      <div style="text-align: center;">
                        <span style="font-weight: bold;">Miscellaneous</span>
                      </div>
                      
                      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                        <tr>
                          <td style="vertical-align: top;">
                            :retab
                          </td>
                          
                          <td style="vertical-align: top;">
                            Change tabs to correct spaces in current file
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            ,cd
                          </td>
                          
                          <td style="vertical-align: top;">
                            Change cwd to dir of current file
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            ,g
                          </td>
                          
                          <td style="vertical-align: top;">
                            Prompt to grep in subdirectories for a pattern (:Grep)
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            <f3>
                          </td>
                          
                          <td style="vertical-align: top;">
                            Pass current file through Scalariform, formatting it (:Autoformat)
                          </td>
                        </tr>
                      </table>
                      
                      <div style="text-align: center;">
                        <span style="font-weight: bold;">Search</span>
                      </div>
                      
                      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                        <tr>
                          <td style="vertical-align: top;">
                            /
                          </td>
                          
                          <td style="vertical-align: top;">
                            Search for expression forwards
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            ?
                          </td>
                          
                          <td style="vertical-align: top;">
                            Search for expression backwards
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            n
                          </td>
                          
                          <td style="vertical-align: top;">
                            Next match forwards
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            N
                          </td>
                          
                          <td style="vertical-align: top;">
                            Next match backwards
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            *
                          </td>
                          
                          <td style="vertical-align: top;">
                            Search forward for word under cursor
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            #
                          </td>
                          
                          <td style="vertical-align: top;">
                            Search backward for word under cursor
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            gD
                          </td>
                          
                          <td style="vertical-align: top;">
                            Jump to first occurrence of this word in this file (Goto definition)
                          </td>
                        </tr>
                      </table>
                      
                      <div style="text-align: center;">
                        <span style="font-weight: bold;">Editing</span>
                      </div>
                      
                      <p>
                        c%Change to next matching symbol (see <a href="http://thepugautomatic.com/2014/03/vims-life-changing-c-percent/">this</a>)
                      </p>
                      
                      <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                        <tr>
                          <td style="vertical-align: top;">
                            ct)
                          </td>
                          
                          <td style="vertical-align: top;">
                            Change until the next &#8220;)&#8221; (or any other text object &#8211; see list)
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            di)
                          </td>
                          
                          <td style="vertical-align: top;">
                            Delete inner parentheses
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            ci)
                          </td>
                          
                          <td style="vertical-align: top;">
                            Change inner parentheses
                          </td>
                        </tr>
                        
                        <tr>
                          <td style="vertical-align: top;">
                            vi)i)
                          </td>
                          
                          <td style="vertical-align: top;">
                            Select inner, then expand to next inner
                          </td>
                        </tr>
                      </table>
                    </td>
                  </tr></tbody> </table> 
                  
                  <div style="text-align: center;">
                    <span style="font-weight: bold;">Actions</span>
                  </div>
                  
                  <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                    <tr>
                      <td style="vertical-align: top;">
                        ci
                      </td>
                      
                      <td style="vertical-align: top;">
                        Change inner
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        di
                      </td>
                      
                      <td style="vertical-align: top;">
                        Delete inner
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        vi
                      </td>
                      
                      <td style="vertical-align: top;">
                        Select inner
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        ca
                      </td>
                      
                      <td style="vertical-align: top;">
                        Change all
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        da
                      </td>
                      
                      <td style="vertical-align: top;">
                        Delete all
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        va
                      </td>
                      
                      <td style="vertical-align: top;">
                        Select all
                      </td>
                    </tr>
                  </table>
                  
                  <div style="text-align: center;">
                    <span style="font-weight: bold;">Text Objects (for use with action commands)</span>
                  </div>
                  
                  <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                    <tr>
                      <td style="vertical-align: top;">
                        ( or )
                      </td>
                      
                      <td style="vertical-align: top;">
                        Parenthesis
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        { or }
                      </td>
                      
                      <td style="vertical-align: top;">
                        Curly braces
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        [ or ]
                      </td>
                      
                      <td style="vertical-align: top;">
                        Square brackets
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        < or >
                      </td>
                      
                      <td style="vertical-align: top;">
                        Angle brackets
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        &#8220;
                      </td>
                      
                      <td style="vertical-align: top;">
                        Double quotes
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        &#8216;
                      </td>
                      
                      <td style="vertical-align: top;">
                        Single quote
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        `
                      </td>
                      
                      <td style="vertical-align: top;">
                        Backticks
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        w
                      </td>
                      
                      <td style="vertical-align: top;">
                        Word
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        W
                      </td>
                      
                      <td style="vertical-align: top;">
                        Word with stricter boundaries
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        s
                      </td>
                      
                      <td style="vertical-align: top;">
                        Sentence
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        p
                      </td>
                      
                      <td style="vertical-align: top;">
                        Paragraph
                      </td>
                    </tr>
                    
                    <tr>
                      <td style="vertical-align: top;">
                        t
                      </td>
                      
                      <td style="vertical-align: top;">
                        Tag
                      </td>
                    </tr>
                  </table>
                  
                  <div style="text-align: center;">
                    <span style="font-weight: bold;">XTemplate</span>
                  </div>
                  
                  <table style="text-align: left; width: 100%;" border="1" cellspacing="2" cellpadding="2">
                    <tr>
                      <td style="vertical-align: top;">
                        freespec C-\
                      </td>
                      
                      <td style="vertical-align: top;">
                        Insert ScalaTest FreeSpec template
                      </td>
                    </tr>
                  </table>
                  
                  <p>
                    &nbsp;
                  </p>
                  
                  <h4 style="text-align: center;">
                    Tmux
                  </h4>
                  
                  <table width="100%" border="1">
                    <tr>
                      <td>
                        <table width="100%" border="1">
                          <tr>
                            <td>
                              C-a C-up, C-a C-left, C-a C-right
                            </td>
                            
                            <td>
                              resize by 1 row/column
                            </td>
                          </tr>
                          
                          <tr>
                            <td style="vertical-align: top;">
                              C-a C-down
                            </td>
                            
                            <td style="vertical-align: top;">
                              resize smaller by 1 row
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              tmux new-session -s work
                            </td>
                            
                            <td>
                              Start a new session
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              tmux attach-session -t work
                            </td>
                            
                            <td>
                              Attach to an existing session
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a $
                            </td>
                            
                            <td>
                              rename the current session
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a (
                            </td>
                            
                            <td>
                              previous session
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a )
                            </td>
                            
                            <td>
                              next session
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a L
                            </td>
                            
                            <td>
                              last (previously used) session
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a s
                            </td>
                            
                            <td>
                              choose a session from a list
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a c
                            </td>
                            
                            <td>
                              create a new window
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a 1 &#8230;
                            </td>
                            
                            <td>
                              switch to window 1, &#8230;, 9, 0
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a p
                            </td>
                            
                            <td>
                              previous window
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a n
                            </td>
                            
                            <td>
                              next window
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a l
                            </td>
                            
                            <td>
                              last (previously used) window
                            </td>
                          </tr>
                        </table>
                      </td>
                      
                      <td>
                        <table width="100%">
                          <tr>
                            <td>
                              C-a w
                            </td>
                            
                            <td>
                              choose window from a list
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a left
                            </td>
                            
                            <td>
                              go to the next pane on the left
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a right
                            </td>
                            
                            <td>
                              (or one of these other directions)
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a o
                            </td>
                            
                            <td>
                              go to the next pane (cycle through all of them)
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a ;
                            </td>
                            
                            <td>
                              go to the last (previously used) pane
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a q
                            </td>
                            
                            <td>
                              Briefly display the pane indicies
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a M-down
                            </td>
                            
                            <td>
                              Make current pane 5 lines smaller
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a &#8220;
                            </td>
                            
                            <td>
                              Split horizontally
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a %
                            </td>
                            
                            <td>
                              Split vertically
                            </td>
                          </tr>
                          
                          <tr>
                            <td>
                              C-a x
                            </td>
                            
                            <td>
                              Close current pane
                            </td>
                          </tr>
                          
                          <tr>
                            <td style="vertical-align: top;">
                              C-a [
                            </td>
                            
                            <td style="vertical-align: top;">
                              Enter scroll mode (j/k to move<br /> up/down, RETURN to exit)
                            </td>
                          </tr>
                        </table>
                      </td>
                    </tr>
                  </table>

 [1]: https://github.com/michaelpnash/vi-for-scala